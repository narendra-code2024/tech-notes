---
name: note-architect
description: Synthesizes raw lecture notes, video subtitles, reading materials, or simple topics into high-fidelity technical notes following official project standards.
---

# Note Architect Skill

Create a new technical note from any source: a topic name, raw lecture notes, rough jottings, video subtitles, or documentation. The synthesized note must fully comply with the canonical standards in @.agents/rules/standards.md; read that file first and treat it as the single source for all structure, formatting, and end-of-file requirements.

## Synthesis Process
1. **Research (if needed)**: If only a topic name is given, use web search and official documentation (e.g., Spring.io, Nodejs.org) to gather accurate, current details.
2. **Analyze Input**: Extract the core concepts, code snippets, and operational tips from the raw input or research results, cleaning transcription noise (e.g. from video subtitles) and discarding off-topic filler.
3. **Structure & Density**: Map the content to the mandatory Content Progression defined in the standards. Consolidate related subtopics and code examples to prevent boilerplate and file bloating.
4. **Write & Finalize**: Produce the complete note in full compliance with @.agents/rules/standards.md. Ensure all prose is highly dense, trust the reader's experience, and include the required end-of-file `## Q&A` and `## Quick Revision Cheat Sheet` sections.
