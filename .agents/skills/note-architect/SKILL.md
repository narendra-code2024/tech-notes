---
name: note-architect
description: Synthesizes raw lecture notes, video subtitles, reading materials, or simple topics into high-fidelity technical notes following official project standards.
---

# Note Architect Skill

When asked to create a new note from any source (topic name, lecture notes, subtitles, or docs), follow the mandatory structural flow defined in `@.agents\rules\standards.md`.

## Synthesis Process
1. **Research (If needed)**: If only a topic name is provided, use **web search** and **official documentation** (e.g., Spring.io, Nodejs.org) to gather the latest technical details.
2. **Analyze Input**: Extract core technical concepts, code snippets, and operational tips from the provided raw data or research results.
3. **Structure**: Map extracted info to the mandatory flow (e.g., Fundamentals → Setup → Usage → Production Considerations).
4. **Scaffold**: Apply the official **Scaffolding Template** below.
5. **Finalize**: Generate `## Q&A` and `## Quick Reference`.

---

## Scaffolding Template

1. **Headerless Intro**: Start with `---`, followed by a high-signal overview of the topic (Fundamentals).
2. **Main Content (`##`)**:
   - Move logically from Concept → Setup → Usage → Production Considerations.
   - Use `---` only between these major sections.
3. **Subsections**:
   - Avoid **thin sections**. A section must have sufficient substance and "logical weight" to justify its own heading.
   - If content is minimal, **logically flatten** it into bolded bullets under a relevant parent section or consolidate related brief topics into a single comprehensive subsection.
   - Use `**Term**: Description` format for all definitions.
4. **End-of-File**:
   - Include a `## Q&A` section with formal Bold Question + 1-3 sentence Answer.
   - Include a `## Quick Reference` 2-column table if the topic is reference-heavy.

---

## Input Sources Handled
- **Simple Topic Names**: Researched via web search and official docs for high-fidelity accuracy.
- **Raw Lecture/Meeting Notes**: Structured into clean technical sections.
- **Video Subtitles**: Cleaned of transcription noise and synthesized into logic-based flows.
- **Documentation/Articles**: Summarized and formatted into the project standard.

## Instructions
Generate the complete Markdown content for the requested topic. Ensure all code examples use real-world domain names (e.g., `OrderService`, `PaymentProcessor`).
