## Encoding

- 1 byte = 8 bits, representing values **0–255** (decimal) or **00–FF** (hex)
- Bytes are how computers store everything — text, images, tokens, passwords

When we call `randomBytes(32)`, we get 32 raw bytes — just numbers between 0–255. That raw data is **not human-readable**, so to use it as a string (in URLs, headers, databases) we **encode** it into text:

```javascript
const crypto = require('crypto');
const rawBytes = crypto.randomBytes(32);
// <Buffer 3a f1 9c 04 b2 ... 28 more bytes>  — not a string

rawBytes.toString('hex');    // → "3af19c04b2..." (64 chars)
rawBytes.toString('base64'); // → "OvGcBLI..."    (~44 chars)
```

Encoding changes the representation, **not** the data. The underlying entropy is still 32 bytes = 256 bits.

> Encoding is **not encryption**: it's just text representation. Anyone can decode it; there's no secret key.

### Hex Encoding

Represents each byte as **2 hexadecimal characters** (0–9, a–f). 1 byte = 2 hex chars; 32 bytes = 64 hex chars.

```
Raw byte:  0xAF (decimal 175)  →  hex "af"
Raw byte:  0x03 (decimal 3)    →  hex "03"
```

```javascript
crypto.randomBytes(32).toString('hex');
// "a4e321556d9f8b2c..."  (64 characters)
```

|Pros|Cons|
|---|---|
|Simple, predictable length|2x size increase|
|Only uses `0-9`, `a-f`|Less compact than Base64|
|Safe in URLs without encoding||

**Common uses:** Token display, hash representation, debug output, database storage.

### Base64 Encoding

Represents every **3 bytes** as **4 characters** using `A-Z`, `a-z`, `0-9`, `+`, `/` and `=` for padding. 32 bytes = ⌈32/3⌉ × 4 = **44 characters**.

```
Raw bytes: [72, 101, 108]  (ASCII: "Hel")  →  Base64 "SGVs"
```

```javascript
crypto.randomBytes(32).toString('base64');
// "OvGcBLKx4pQ..."  (~44 characters)
```

|Pros|Cons|
|---|---|
|More compact than hex|Uses `+`, `/`, `=` (not URL-safe)|
|~33% size increase (vs 100% for hex)|Slightly harder to read|
|Widely supported|Needs URL-safe variant for URLs|

**Common uses:** JWT tokens, email attachments (MIME), API keys, image embedding in HTML (`data:image/png;base64,...`).

### Base64URL Encoding

A **URL-safe variant** of Base64. Replaces characters that break URLs: `+` → `-`, `/` → `_`, `=` removed (no padding).

```
Standard Base64:  "abc+def/ghi="
Base64URL:        "abc-def_ghi"
```

```javascript
crypto.randomBytes(32).toString('base64url');
// "OvGcBLKx4pQ..."  (~43 characters, no padding)
```

|Pros|Cons|
|---|---|
|Safe in URLs and query params|Not all languages have built-in support|
|Compact like Base64|Less common than standard Base64|
|No padding `=` characters||

**Common uses:** JWT tokens (all 3 JWT parts are Base64URL encoded), OAuth tokens, URL-safe identifiers.

### URL Encoding (Percent Encoding)

**Different purpose.** Doesn't encode raw bytes — makes **existing text** safe for URLs by replacing reserved characters (`?`, `&`, `=`, `/`, `#`, `@`, space, etc.) with `%XX` where XX is the hex value of the character's byte.

```
Space → %20    @ → %40    & → %26    = → %3D
Password@123  →  Password%40123
```

```
Without encoding (broken):
https://api.com/search?q=hello world&lang=en
                            ↑ space breaks URL

With encoding:
https://api.com/search?q=hello%20world&lang=en
```

```javascript
encodeURIComponent("Password@123");   // "Password%40123"
decodeURIComponent("Password%40123"); // "Password@123"
```

|Pros|Cons|
|---|---|
|Makes any text URL-safe|Can significantly increase size|
|Standard across all browsers/servers|Not meant for encoding raw binary|
|Reversible||

**Common uses:** Query parameters, form data (`application/x-www-form-urlencoded`), any user input placed in URLs.

### Encoding Comparison at a Glance

|Encoding|Purpose|Input|32 bytes becomes|URL Safe?|
|---|---|---|---|---|
|**Hex**|Bytes → text|Raw bytes|64 characters|Yes|
|**Base64**|Bytes → text|Raw bytes|~44 characters|No (`+`, `/`, `=`)|
|**Base64URL**|Bytes → text (URL safe)|Raw bytes|~43 characters|Yes|
|**URL Encoding**|Text → URL-safe text|Existing string|Varies (larger)|Yes (that's the point)|

Hex / Base64 / Base64URL answer: "How do I represent binary data as text?" URL encoding answers: "How do I put this text safely in a URL?"

### Use Case — Secure Random Token Generation

The most common application of bytes + encoding: generating cryptographically secure tokens (API keys, session IDs, password reset links). Generate raw bytes from a CSPRNG, then encode to a string.

**Node.js:**

```javascript
const crypto = require('crypto');
const token = crypto.randomBytes(32).toString('hex');
// 64-character hex string, 256 bits of entropy
```

**Java:**

```java
SecureRandom random = new SecureRandom();
byte[] bytes = new byte[32];
random.nextBytes(bytes);
String token = HexFormat.of().formatHex(bytes);
// 64-character hex string, 256 bits of entropy
```

The flow: `randomBytes(32)` produces 32 cryptographically-secure raw bytes → `.toString('hex')` converts each byte to 2 hex characters → 64-character string like `"a4e321556d9f..."`.

### Java `char` vs Bytes — Common Confusion

> "A character is 2 bytes in Java — so doesn't 64 characters = 128 bytes?"

|Concept|Size|
|---|---|
|Raw random data|32 bytes|
|Hex string length|64 characters|
|Java memory for that string|128 bytes (because `char` = 2 bytes in UTF-16)|
|**Actual entropy / security**|**256 bits (unchanged)**|

Java `char` = 2 bytes is an **internal memory representation** detail. The hex string is a **human-readable representation** of the original bytes. The security strength is determined by the **original random bytes**, not how they're stored in memory.

---

## bcrypt — Password Hashing & Hash Anatomy

Hashing vs encryption — important distinction first:

- **Encryption (two-way)**: can be **encrypted** and **decrypted** with a key. Used for data transmission (HTTPS/TLS), file protection. Examples: AES, RSA.
- **Hashing (one-way)**: **cannot be reversed**. Used for password storage, data integrity. Examples: bcrypt, SHA256, Argon2.

> **Critical rule:** Passwords must be hashed, NEVER encrypted. If passwords are encrypted, whoever has the key can decrypt all of them.

**bcrypt** is a one-way password hashing algorithm based on the Blowfish cipher. Includes automatic salting and is intentionally slow to resist brute-force attacks. It has built-in salt generation, a configurable cost factor (adjustable slowness), is battle-tested and widely supported, and is resistant to rainbow table attacks.

### Hash Anatomy

Every bcrypt hash is exactly **60 characters** and embeds the algorithm, cost factor, salt, and the actual hash digest:

```
$2a$10$gOBiDbhQSYpO1zpWUdQqS.JjdH2QfFwBXzc8u/Z30S2DU3/mmvjZu
```

(This is the hash of `Password@123`.)

Format: `$algorithm$cost$salt+hash`

|Part|Value|Meaning|
|---|---|---|
|`$2a$`|Algorithm|bcrypt version (variants: `2a`, `2b`, `2y`)|
|`10`|Cost factor|2^10 = 1,024 hashing rounds|
|`gOBiDbhQSYpO1zpWUdQqS.`|Salt|22 characters, randomly generated|
|`JjdH2QfFwBXzc8u/Z30S2DU3/mmvjZu`|Hash|31 characters, the actual hash output|

> Total: `$2a$` (4) + `10` (2) + `$` (1) + salt (22) + hash (31) = 60 characters. Salt and hash are concatenated with no separator between them.

---

## bcrypt Parameters — Salt & Cost Factor

The hash structure above embeds two configurable parameters: a per-hash **salt** (defeats rainbow tables) and a **cost factor** (defeats brute-force).

### Salt

- A **random value** generated automatically by bcrypt
- **Unique per hash**: even for the same password
- **Stored inside the hash** itself (not separately)

Without salt, `Password@123` always hashes to the same output, so an attacker can pre-compute hashes (rainbow table attack). With salt:

```
Password@123 + salt_A → Hash_A
Password@123 + salt_B → Hash_B  (completely different)
```

> Two users with the same password will have **completely different** hashes.

### Cost Factor

```
$2a$10$  →  cost = 10  →  2^10 = 1,024 rounds
$2a$12$  →  cost = 12  →  2^12 = 4,096 rounds
$2a$14$  →  cost = 14  →  2^14 = 16,384 rounds
```

|Cost|Rounds|Approx. Time per Hash (typical hardware)|
|---|---|---|
|10|1,024|~50–100ms|
|12|4,096|~200–400ms|
|14|16,384|~800ms–1.5s|

> Rough estimates — actual times depend on CPU, implementation, and language.

**Why slowness = security:** legitimate user hashes once during login (100ms is fine); attacker must hash *billions* of guesses (100ms each is devastating).

**Recommendation:** **10–12** for most applications. Increase over time as hardware gets faster.

---

## How Password Verification Works

**At registration:** server hashes the raw password and stores the result.

```
User enters:   Password@123
Server runs:   hash = bcrypt("Password@123")
Server stores: $2a$10$gOBiDbhQSYpO1zpWUdQqS.JjdH2QfFwBXzc8u/Z30S2DU3/mmvjZu
```

**At login:** server re-hashes the submitted password using the salt + cost extracted from the stored hash, then compares.

```
User enters: Password@123

System does:
  1. Read stored hash from DB
  2. Extract: algorithm (2a), cost (10), salt (gOBiDbhQSYpO1zpWUdQqS.)
  3. Run: bcrypt("Password@123", extracted_salt, cost=10)
  4. Compare new hash with stored hash
  5. Match → login success
```

> **No decryption ever happens.** Verification = re-hash with same salt → compare results.

Framework one-liners:

```javascript
// Node.js
const bcrypt = require('bcrypt');
const isMatch = await bcrypt.compare(inputPassword, storedHash);
```

```java
// Java (Spring Security)
passwordEncoder.matches(rawPassword, storedHash);
```

```php
// Laravel (PHP)
Hash::check($enteredPassword, $storedHash);
```

---

## bcrypt vs SHA256 vs Argon2

| Feature              | SHA256                 | bcrypt               | Argon2                 |
|----------------------|------------------------|----------------------|------------------------|
| Speed                | Very fast              | Intentionally slow   | Intentionally slow     |
| Built-in salt        | No                     | Yes                  | Yes                    |
| Configurable cost    | No                     | Yes                  | Yes                    |
| Memory hard          | No                     | No                   | Yes                    |
| GPU attack resistant | No                     | Partial              | Strong                 |
| Safe for passwords   | No                     | Yes                  | Yes                    |
| Status               | Wrong tool for the job | Legacy, still secure | Current recommendation |

> **Never use plain SHA256 for password storage.** bcrypt is still secure and widely deployed; Argon2 is the modern strongest choice (memory-hard).

---

## What If Attacker Steals the Database?

The attacker gets only the bcrypt hashes — `$2a$10$gOBiDbhQSYpO1zpWUdQqS.JjdH2QfFwBXzc8u/Z30S2DU3/mmvjZu`. They **cannot** reverse hashes back to plaintext, and they **cannot** use rainbow tables (each hash has a unique salt). The only avenue is brute-force: guess → hash → compare → repeat.

**What slows them down**: **bcrypt's intentional slowness**: each guess takes ~100ms at cost=10
- **Unique salt per hash**: must attack each user's hash individually (no shared rainbow tables)
- **High cost factor**: every +1 doubles attacker work
- **Strong user passwords**: harder to guess in the first place

**Attacker math** at cost=10 (~10–100 guesses/sec/hash on typical hardware):

- 4-char simple password: minutes to hours
- 8-char complex password (mixed case + symbols): months to years
- 12+ char random passphrase: practically unbreakable with current hardware

> GPU attacks are less effective against bcrypt than against SHA256, but dedicated hardware (FPGAs) can speed things up — this is where Argon2's memory-hardness helps.

---

## Password Storage — Best Practices

- Use bcrypt or Argon2
- Never store plaintext passwords
- Never log passwords
- Use cost factor 10–12 (increase over time)
- Never use MD5 or plain SHA for passwords

> JWT-side concerns (token transport, HttpOnly vs localStorage, browser-vs-microservice split) live in [5.6 Understanding JWT](<5.6. Understanding JWT.md>) and [5.7 JWT Implementation](<5.7. JWT Implementation.md>) — this appendix focuses on byte-level fundamentals.


