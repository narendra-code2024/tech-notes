---
name: note-reviewer
description: Audits a technical note against the project's official Technical Note Standards. Flags violations in bolding, separators, and structural integrity.
---

# Note Reviewer Skill

When invoked on a file, perform a rigorous audit based on `@.gemini\rules\standards.md`.

## Audit Checklist
1. **Structural Integrity**:
   - Verify file starts with `---`.
   - Ensure `---` only exists between major `##` sections (never `###`).
   - Check for **Thin Sections**: Identify sections with minimal content that lack sufficient "logical weight" to justify a standalone heading. Flag these for flattening into bolded bullets or consolidation.
   - Check for "Echo Headings": Ensure no `## What is...` headers; intro must be headerless at the top.

2. **Formatting & Visuals**:
   - **Bolding Noise**: Flag if terms are bolded more than once per section or if entire phrases are bolded.
   - **Definition Separators**: Ensure all definitions use a colon (`:`) after the bolded term, not a dash (`—`) or hyphen (`-`).
   - **Code Blocks**: Ensure all code blocks have language tags and use real-world domain names.

3. **Required Sections**:
   - Ensure the note ends with `## Q&A` and optionally `## Quick Reference`.

## Output Format
Provide a concise list of "Violations" and "Suggested Fixes". If the note passes all checks, respond with "✅ Note matches all Project Standards."
