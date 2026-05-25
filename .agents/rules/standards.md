
## Technical Note Standards

Canonical declarative standards for all technical notes in this vault. These rules apply to both content creation and quality review.

## 1. Content Progression
- **Mandatory Flow**: Fundamentals → Production-ready configuration → Real-world industry practices.

## 2. Structural Requirements
- **Separators**: Use `---` only between major `##` sections. Never use `---` to separate `###` subsections.
- **Headings**: `##` (major), `###` (minor). Avoid deeper nesting. **Never use numbers in headings** (e.g., use `## Setup`, not `## 1. Setup`).
- **Anti-patterns to avoid**:
  - **Echo-headings**: No `## What is <Title>?`. Merge intro into the top of the file (no header).
  - **Thin sections**: Avoid sections with minimal content that don't justify a standalone heading. A section must have significant "logical weight" to exist independently. If the information is brief, **logically flatten** it into bolded bullets under a relevant parent section or consolidate it with other related content.
  - **Single-child wrapper**: If `## A` only contains `### B`, promote `B` and drop `A`.

## 3. Formatting & Visuals
- **Bolding**: Keep bolding minimal. Bold foundational terms only once per section. No visual "noise" from over-bolding.
- **Definition Separator**: Always use a colon (`:`) between a bolded term and its definition.
- **Syntactic Context**: Reserved exclusively for `**Term**: Description` pairs. Do not use the colon separator for narrative emphasis or general punctuation within a sentence.
- **Code**: Tag language explicitly (e.g., ` ```java `). Prefer concise, short variable names (e.g., `a`, `b`, `name`, `val`) to maintain high density; avoid verbose names (e.g., `autoBoxedInteger`). Keep descriptive class names and meaningful literals (e.g., `"Alice"`) to preserve context.
- **Table Pipes & Formatting**: Use the HTML entity `&#124;` for any pipe characters (`|`) inside table cells to prevent rendering breaks. **Always pretty-print and vertically align the columns and pipe characters (`|`)** of markdown tables using padding spaces to ensure raw source-code readability.
- **Tone & Terminology**: Maintain a direct, professional tone. NEVER use informal filler or words like "gotcha," "nuance," "pitfall," or "deep-dive." Use "Note:" or "Special Case(s):" instead.

## 4. Cross-Referencing & Callouts
- **Links**: Use standard markdown `[Text](<File.md>)`. Wiki-links (`[[]]`) are strictly forbidden.
- **Economy**: Max 1 link per target per section. Links must be load-bearing.
- **Callouts (`> `)**: Reserved exclusively for Notes, Cautions, and Cross-references. Do not use for general definitions. If a callout contains multiple unrelated points or distinct scenarios, use a bulleted list for readability.

## 5. Standard End-of-File Sections
- **Q&A**: Must use sequential numbering (1., 2.), a formal bold question, and a 1-3 sentence answer. **Answers must not be indented** (flush left).
- **Quick Revision Cheat Sheet**: 2-column table (`Concept | Remember`). Max 12 rows. This section title is mandatory for all summaries.
