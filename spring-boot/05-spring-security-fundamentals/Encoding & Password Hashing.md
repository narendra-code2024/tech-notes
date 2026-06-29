Two distinct fundamentals behind auth tokens and credential storage: encoding represents raw bytes as text (reversible, no secret), and hashing stores passwords one-way (irreversible).

---

## Encoding

Encoding changes the representation of data, not the data itself: 32 random bytes stay 256 bits of entropy whether shown as hex or Base64. It is not encryption; anyone can decode it because there is no key.

| Encoding     | Purpose                        | Input           | 32 bytes becomes | URL-safe?              |
| ------------ | ------------------------------ | --------------- | ---------------- | ---------------------- |
| Hex          | Bytes to text.                 | Raw bytes       | 64 chars         | Yes.                   |
| Base64       | Bytes to text (compact).       | Raw bytes       | ~44 chars        | No (`+`, `/`, `=`).    |
| Base64URL    | Bytes to text, URL-safe.       | Raw bytes       | ~43 chars        | Yes.                   |
| URL encoding | Make existing text URL-safe.   | Existing string | Varies (larger)  | Yes (that is the point).|

Hex maps 1 byte to 2 chars (doubles size). Base64 maps 3 bytes to 4 chars (~33% growth). Base64URL is Base64 with `+` to `-`, `/` to `_`, and no `=` padding, and is what all three JWT parts use. URL (percent) encoding is a different job: it makes existing text safe in a URL by replacing reserved characters (`@` to `%40`, space to `%20`), not for encoding binary.

Generate secure tokens from a CSPRNG, then encode:

```java
byte[] bytes = new byte[32];
new SecureRandom().nextBytes(bytes);
String token = HexFormat.of().formatHex(bytes);   // 64-char hex, 256 bits of entropy
```

---

## Password Hashing

Hashing and encryption are not interchangeable:

- **Encryption** is two-way: encrypt and decrypt with a key (AES, RSA). Used for transport (TLS) and file protection.
- **Hashing** is one-way and cannot be reversed (bcrypt, Argon2, SHA-256). Used for password storage and integrity.

> **Note**: passwords must be hashed, never encrypted; whoever holds an encryption key could decrypt every password at once.

**bcrypt** is a one-way password hash based on the Blowfish cipher, with automatic per-hash salting, a configurable cost factor, and resistance to rainbow-table attacks. Every bcrypt hash is exactly 60 characters and embeds the algorithm, cost, salt, and digest:

```
$2a$10$gOBiDbhQSYpO1zpWUdQqS.JjdH2QfFwBXzc8u/Z30S2DU3/mmvjZu
```

| Part      | Value                             | Meaning                                  |
| --------- | --------------------------------- | ---------------------------------------- |
| `$2a$`    | Algorithm                         | bcrypt version (variants `2a`, `2b`, `2y`). |
| `10`      | Cost factor                       | 2^10 = 1,024 rounds.                     |
| 22 chars  | `gOBiDbhQSYpO1zpWUdQqS.`           | Salt, randomly generated.                |
| 31 chars  | `JjdH2QfFwBXzc8u/Z30S2DU3/mmvjZu`  | The hash digest.                         |

Layout is `$2a$` (4) + cost (2) + `$` (1) + salt (22) + digest (31) = 60 chars; salt and digest are concatenated with no separator.

> **Note**: bcrypt silently truncates the password to its first 72 bytes, so two passwords sharing a 72-byte prefix collide. For longer inputs, pre-hash (e.g. SHA-256) before bcrypt, or use Argon2.

### Salt

A random value bcrypt generates automatically, unique per hash, and stored inside the hash itself. It defeats rainbow tables: the same password produces a different digest per salt, so two users with identical passwords store different hashes and each must be attacked individually.

### Cost Factor

The exponent controlling work: `$2a$<cost>$` means 2^cost rounds. Higher cost means slower hashing and more brute-force resistance, and each +1 doubles the work. A user hashes once at login (100ms is fine) while an attacker must hash billions of guesses, so slowness is the defense. Use 10 to 12 and raise it as hardware improves.

| Cost | Rounds | Approx. time per hash |
| ---- | ------ | --------------------- |
| 10   | 1,024  | ~50 to 100ms          |
| 12   | 4,096  | ~200 to 400ms         |
| 14   | 16,384 | ~800ms to 1.5s        |

### Verification

Verification never decrypts. At registration the server stores `bcrypt(rawPassword)`. At login it reads the stored hash, extracts the embedded cost and salt, re-hashes the submitted password with them, and compares.

```java
passwordEncoder.matches(rawPassword, storedHash);   // Spring Security
```

> **Note**: Spring Boot's default `PasswordEncoderFactories.createDelegatingPasswordEncoder()` stores an `{id}` prefix (e.g. `{bcrypt}$2a$...`), so the app can verify legacy hashes and migrate algorithms without breaking existing users. A bare `new BCryptPasswordEncoder()` writes no prefix.

---

## bcrypt vs SHA-256 vs Argon2

| Feature              | SHA-256                | bcrypt               | Argon2                 |
| -------------------- | ---------------------- | -------------------- | ---------------------- |
| Speed                | Very fast              | Intentionally slow   | Intentionally slow     |
| Built-in salt        | No                     | Yes                  | Yes                    |
| Configurable cost    | No                     | Yes                  | Yes                    |
| Memory-hard          | No                     | No                   | Yes                    |
| GPU-attack resistant | No                     | Partial              | Strong                 |
| Safe for passwords   | No                     | Yes                  | Yes                    |
| Status               | Wrong tool            | Secure, widely used  | Modern strongest choice |

A stolen database yields only salted hashes: they cannot be reversed, and the unique per-hash salt makes rainbow tables useless, leaving only per-user brute force at bcrypt's deliberate cost.

> **Note**: never use plain SHA-256 (or MD5) for password storage; it is built for speed, which is exactly what an attacker wants. bcrypt remains secure; Argon2id is the memory-hard modern recommendation, available as `Argon2PasswordEncoder`.

---

## Q&A

1. **Why is the salt stored inside the hash rather than kept secret?**
The salt is not a secret; its job is to make identical passwords hash differently, defeating rainbow tables. Verification needs the original salt to re-hash the submitted password, so it is embedded in the 60-char string alongside the digest.

2. **What is bcrypt's 72-byte limit?**
bcrypt only consumes the first 72 bytes of the password and silently truncates the rest, so longer passwords sharing a 72-byte prefix collide. Pre-hash with SHA-256 before bcrypt, or use Argon2, when inputs can exceed that.

3. **Why does Spring store a `{bcrypt}` prefix on the hash?**
The default `DelegatingPasswordEncoder` reads the `{id}` prefix to pick the matching encoder, letting an app verify legacy hashes and migrate to a stronger algorithm without forcing every user to reset their password.

---

## Quick Revision Cheat Sheet

| Concept           | Remember                                                              |
| ----------------- | -------------------------------------------------------------------- |
| Encoding          | Representation, not encryption; reversible, no key.                  |
| Hex               | 1 byte to 2 chars; doubles size; URL-safe.                           |
| Base64            | 3 bytes to 4 chars; ~33% growth; `+`, `/`, `=` not URL-safe.         |
| Base64URL         | `+` to `-`, `/` to `_`, no padding; used by JWT.                     |
| Hashing           | One-way; passwords hashed, never encrypted.                          |
| bcrypt hash       | 60 chars: `$2a$<cost>$` + 22-char salt + 31-char digest.             |
| Salt              | Auto, per-hash, embedded; defeats rainbow tables.                    |
| Cost factor       | 2^cost rounds; 10 to 12 typical; +1 doubles work.                    |
| 72-byte limit     | bcrypt truncates beyond 72 bytes; pre-hash or use Argon2.            |
| Verification      | Re-hash with embedded salt and compare; no decryption.              |
| Spring encoder    | `DelegatingPasswordEncoder` writes `{bcrypt}` for migration.        |
| Algorithm choice  | SHA-256 never; bcrypt secure; Argon2id strongest (memory-hard).     |