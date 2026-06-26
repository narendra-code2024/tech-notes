# Importance Weighting

Companion to `standards.md`. `standards.md` owns the *principle* (Importance-Weighted Coverage); this file holds the *specifics* so the canonical file stays principle-level. Keep this lean: a rubric plus a seed list of recurring low-value subtopics, not a frozen ranking of every note.

## Tiers

Tier the topic, then each subtopic within it.

- **Core**: high interview frequency and daily real-world use. Expand; this is where depth belongs.
- **Useful**: real but situational. Keep tight, a few lines or a consolidated block.
- **Trivia**: rarely written by a 3+ yr dev, legacy, or interview-only curiosity. Compress to a mention or cut, even when the existing prose is clean and correct.

The per-note tiering stays a reviewable step in the report, not a hardcoded table here. Override in the report when a specific note warrants it.

## Always-Compress Subtopics

Default these to trivia unless the note's whole topic is about them. Compress to a few lines or a one-line mention.

- Motivation framing: "pre-Java-X pain" / "why the feature was added" history blocks. A 3+ yr dev knows why. Fold one useful sentence into the lead, cut the rest.
- `Externalizable`, custom `writeObject`/`readObject`, `readResolve` singletons (Serialization).
- Generic constructors; raw-type and pre-generics legacy behavior beyond a single caution (Generics).
- Anonymous-class forms when a lambda or method reference is the modern equivalent.
- Legacy `java.io.File` beyond a short comparison once `java.nio.file` is covered.
- Scheduler-hint APIs with no guarantee (`Thread.yield`, thread priorities) beyond a one-line mention.

## Always-Expand Signals

Spend space here even if the original note was thin on them.

- Security constraints (untrusted deserialization, injection, unsafe reflection).
- Concurrency correctness (visibility, happens-before, atomicity, deadlock ordering).
- Compiler/JVM behavior that surprises (type erasure limits, autoboxing identity, `finally` over `return`).
- Modern, currently-recommended APIs and the version they arrived in.

## Currency

Version-gated claims (`Java X+` tags, JEP status, deprecated or removed APIs) must reflect current behavior. Verify with web search when uncertain rather than asserting from memory.