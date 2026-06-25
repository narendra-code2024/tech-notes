# Technical Note Standards

Canonical declarative standards for all technical notes in this vault. These rules apply to both content creation and quality review.

## Content Progression
- **Mandatory Flow**: Fundamentals → Production-ready configuration → Real-world industry practices.
- **Pedagogical Integrity**: A note must not use or reference features that are introduced in a later note (e.g., a fundamentals note must not rely on advanced constructs like records, sealed classes, or pattern matching that belong to later, more advanced notes). Keep the cognitive load strictly appropriate for the note's level.
- **Definition Progression**: Open any definition or lead (file-level or section-level) with the plain, language-agnostic concept stated as one complete sentence, then layer in the OOP/language-specific terminology, keywords, and rules. Do not front-load several technical terms at once (e.g. define what inheritance *is* before naming `extends`, IS-A, `instanceof`, and single-inheritance in the same breath), and never open with a sentence fragment. Progress general → specific. A main definition must run a maximum of 2 lines; if additional context is necessary, split it into a separate paragraph (also max 2 lines) after a blank line.
- **Conciseness & Information Density**: Sentences must be highly optimized, punchy, and direct. Eliminate wordiness, passive voice, and redundant descriptions. Keep explanations compact while retaining full technical depth. To minimize structural boilerplate (e.g., repeating imports, class declarations, and harness methods), consolidate sibling concepts and examples under a parent section into a single, unified code block rather than splitting them into separate blocks for each minor subtopic.
- **High-Yield Filtering (3+ Exp Dev Standard)**: Actively prune all specialized, low-yield, or rarely-used platform APIs and configurations that do not add real-world value for a developer with 3+ years of experience, unless they are highly critical from a standard technical interview perspective. Exclude niche operations, redundant examples, and third-party library clutter to keep guides exceptionally dense, focused, and professional. Trust the reader's professional experience: completely bypass introductory prose, syntax tutorials, and standard definitions of basic concepts. Focus exclusively on compiler constraints, validation rules, JVM behaviors, and performance/security details.

## Structural Requirements
- **Separators**: Use `---` only between major `##` sections. Never use `---` to separate `###` subsections.
- **File Start**: Open with genuine content, decided by whether the topic has a natural lead (a core definition or relationship):
  - **Has a lead** → state it headerless at the top, as long as the content warrants (no padding), then `---` before the first `##`.
  - **No single lead** (a set of distinct sub-topics) → open directly with the first `## section`.
  - **Never** a filler or meta intro that merely lists what the note covers ("This note covers…").
- **Heading Hierarchy**: Choose the tier by content weight, not by topic importance:
  - `##` **Major section**: a distinct top-level topic with substantial content. Separated by `---`.
  - `###` **Minor section**: a sub-topic with real substance, multiple sentences, its own sub-points, or a meaty code block. Avoid deeper nesting; never use `####`.
  - `- **Term**:` **Bolded bullet**: the lowest tier, for a concept worth only a sentence or two, a definition, or one of several short related items. Below this, use nested sub-bullets, a table, or a consolidated code block, never a deeper heading.
  - **Tiers are skippable, not sequential**: A `##` may contain prose or bolded bullets directly, `###` is optional and used only when a sub-topic earns it. Never insert an empty or thin `###` just to "reach" the bullets beneath a `##`.
  - **Rule of thumb**: if a `###` would hold only ~1–2 sentences, demote it to a bolded bullet. Never use numbers in headings (e.g., `## Setup`, not `## 1. Setup`).
- **Code Example Quality**: Pitfall demonstrations (like fall-through or dangling-else) must clearly contrast the **Accidental Bug** and **Intentional Use Case** using a realistic, simple, and factually accurate scenario (e.g., using correct calendar weeks or user roles, not arbitrary math or placeholders).
- **Anti-patterns to avoid**:
  - **Echo-headings**: No `## What is <Title>?`. Merge intro into the top of the file (no header).
  - **Thin sections**: Avoid sections with minimal content that don't justify a standalone heading. A section must have significant "logical weight" to exist independently. If the information is brief, **logically flatten** it into bolded bullets under a relevant parent section or consolidate it with other related content.
  - **Single-child wrapper**: If `## A` only contains `### B`, promote `B` and drop `A`.
  - **Pseudo-headings**: Do not use a bolded `**Label:**` line as a stand-in for a heading; use a real heading tier, a bolded bullet, or a callout instead.
  - **Logical Purity**: Tables and lists must contain *only* members that genuinely belong to the stated category (e.g., a "direct subclasses" table lists only actual direct subclasses, never unrelated siblings). Do not dilute a category with loosely related entries.
  - **Intra-note redundancy**: Do not teach the same concept or repeat the same code demonstration across multiple sections of one note, keep it in its most relevant section and cross-reference if needed. Fold a lone `**Label**:` + single short snippet into adjacent prose or an existing code block rather than leaving a standalone fragment. Do not restate in prose what an adjacent table or bullet list already encodes (e.g. a one-line "rule" sentence next to a table that captures the same distinction); keep the denser structured form.
  - **Overlapping Tables**: Do not feature multiple overlapping comparison tables (e.g., a table comparing classes vs abstract classes, and another for abstract classes vs interfaces). Consolidate all dimensions into a single, comprehensive comparison table (e.g., `Class vs Abstract Class vs Interface`), and use concise bullet points for specific usage guidelines.
  - **Table of Contents (TOC)**: Table of Contents files (e.g., `<Subject> - Table of Contents.md`) must list only actual `##` and `###` topic headings from their corresponding notes, using concise topic/subtopic names. TOC files should not have references, callouts, verbose descriptions, non-existent headings, or cross-reference links.

## Formatting & Visuals
- **Bolding**: Keep bolding minimal. Bold foundational terms only once per section. No visual "noise" from over-bolding.
- **Definition Separator**: Always use a colon (`:`) between a bolded term and its definition. Reserve this colon exclusively for `**Term**: Description` pairs, never use it for narrative emphasis or general punctuation within a sentence.
- **Code**: Tag every real code block with its *accurate* language (e.g., ` ```java `, ` ```bash `). Leave ASCII diagrams, trees, and flows in a **plain untagged fence** (no language), never apply a real language tag to a diagram (e.g., ` ```bash ` on a Write→Compile→Run flow), and avoid ` ```text ` (it can trigger inconsistent syntax highlighting). Prefer concise, short variable names (e.g., `a`, `b`, `sf` for static fields, `val` for instance fields, `out()` / `show()` for methods) to maintain high density; avoid verbose names (e.g., `staticField`, `autoBoxedInteger`). Keep descriptive class names and meaningful literals (e.g., `"Alice"`) to preserve context.
- **Visual Consolidation over Bullet Lists**: For stateless or minor utility methods (such as `java.lang.Math` operations), prefer consolidating them into a single, comprehensive, well-commented code block rather than splitting them into consecutive bullet items or thin subsections. This eliminates list clutter and provides a unified copy-paste reference.
- **Label vs bullet for code-heavy items**: When **two or more** sibling concepts **each** carry a multi-line code block, give each a standalone `**Term**:` label with a top-level code block, not `- **Term**:` bullets with the blocks indented beneath (which cramps the code). A single bolded bullet with one short snippet is fine.
- **Comment Redundancy Elimination**: Avoid repetitive inline comments in code blocks (e.g., repeating the same exception on every line of an overflow-checked block). Use descriptive, targeted comments explaining *why* a specific line behaves as it does, rather than repeating what the block header already states. Collapse multi-line comments that express a single idea into one line, and cut comments that merely restate the code. Drop variables declared in a snippet but never read. When a code block ends with trailing warning comments (e.g. `// warning ...`), prefer a `> **Note**:` callout after the block instead (still following the single-point-inline vs multiple-points-bullets callout rule).
- **Table Pipes & Formatting**: Use the HTML entity `&#124;` for any pipe characters (`|`) inside table cells to prevent rendering breaks. **Always pretty-print and vertically align the columns and pipe characters (`|`)** of markdown tables using padding spaces to ensure raw source-code readability. Drop any column whose value is identical across all rows (e.g., a constant "Extends Parent?" column), it carries no information.
- **Tone & Terminology**: Maintain a direct, professional tone. NEVER use informal filler or vague/awkward words like "gotcha," "nuance," "pitfall," "treatment," or "deep dive" / "deep-dive" (in any form, hyphenated or spaced). Use "Note:" or "Special Case(s):" instead.
- **Punctuation**: Never use the em-dash (`—`) anywhere, including code comments. Recast with a comma, period, or semicolon; use parentheses only when none of those fit. (Box-drawing `─` and arrows `←`/`→` in ASCII diagrams are not em-dashes and are fine.)
- **No Emojis**: Do not use checkmark (`✅`), cross (`❌`), or warning (`⚠️`) emojis anywhere in the notes (including inside tables, lists, or code comments). These symbols disrupt visual flow and readability. Instead, use standard descriptive text or simple code comment tags (e.g., `// compiles`, `// compile error`, `// OK`, `// invalid`, `// warning`).
- **Paragraph Length**: Keep prose compact. A general explanation or narrative paragraph should run roughly 1-4 lines; if it grows longer or bundles several distinct points, break it into bullets, a bold-label list, or a table instead of a dense wall of text.
- **Visual Spacing**: Bullet lists containing complex nested code blocks or tables must have explicit blank lines **before** and **after** each bullet item (and between the list heading and its nested block) to ensure flawless rendering and visual padding. Separate blocks with a single blank line, never consecutive blank lines, and no trailing blank lines at end of file.

## Cross-Referencing & Callouts
- **Links**: Use standard markdown `[Text](<File.md>)`. Wiki-links (`[[]]`) are strictly forbidden.
- **Economy**: Max 1 link per target per section. Links must be load-bearing.
- **Callouts (`> `)**: Reserved for two labels, each starting with `> ` and the colon placed **outside** the bold (never `> **Note:**` or a bare `**Note**:`):
  - `> **Note**:` for an important inline point or caution.
  - `> **Reference**:` for a pointer to another note/file; the cross-reference link goes here.
  - **Single point**: place it inline on one line, e.g. `> **Note**: a missing classpath entry throws \`ClassNotFoundException\` at runtime.`
  - **Multiple points**: list them as `> -` bullets under the label, not run together in one line:

    ```
    > **Note**:
    > - First point.
    > - Second point.
    ```

  - **Placement**: Callouts (such as `> **Note**:`) must be placed at the very end of their parent section or subsection, never in the middle or between other content blocks.

## Standard End-of-File Sections
- **Q&A**: Must use sequential numbering (1., 2.), a formal bold question, and a 1-3 sentence answer. **Answers must not be indented** (flush left). Answers are prose; a short illustrative code snippet is allowed only when it demonstrates a non-obvious mechanic that prose alone cannot convey as clearly. When an answer compares several distinct items (e.g. `final` vs `finally` vs `finalize`), use `- **Term**:` bullets or a small table instead of a run-on paragraph.
  - *3+ Exp Dev Standard*: Do not include standard textbook definitions or entry-level concepts (e.g., "What is a Scanner?"). Focus strictly on high-yield JVM gotchas, security details, and non-obvious environment behaviors. Cross-note duplicates are strictly forbidden (e.g., do not discuss array printing if a dedicated Arrays note exists).
- **Quick Revision Cheat Sheet**: 2-column table (`Concept | Remember`). Max 12 rows. This section title is mandatory for all summaries. The Concept column is plain text (no bold).
  - *3+ Exp Dev Standard*: Exclude elementary syntax, standard class descriptions, and basic language definitions. The table must act as a dense, high-signal revision card focusing exclusively on structural mechanics, security constraints, and thread-safety details.
