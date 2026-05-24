
## Technical Note Standards

Canonical declarative standards for all technical notes in this vault. These rules apply to both content creation and quality review.

## 1. Content Progression
- **Mandatory Flow**: Fundamentals → Production-ready configuration → Real-world industry practices.
- **Prerequisites**: Must be listed at the top using `> ` callouts.
- **Ops Section**: For heavy topics, a `## Production Considerations` list must precede the Q&A.

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
- **Code**: Tag language explicitly (e.g., ` ```java `). Use real-world domain names (`OrderService`), never `Foo/Bar`.
- **Tables**: Reserved for reference lookups and comparisons, not for narrative descriptions.

## 4. Cross-Referencing & Callouts
- **Links**: Use standard markdown `[Text](<File.md>)`. Wiki-links (`[[]]`) are strictly forbidden.
- **Economy**: Max 1 link per target per section. Links must be load-bearing.
- **Callouts (`> `)**: Reserved exclusively for Notes, Cautions, and Cross-references. Do not use for general definitions.

## 5. Standard End-of-File Sections
- **Q&A**: Must use formal bold question + 1-3 sentence answer. Focus on "Why" and edge cases, not trivia.
- **Quick Reference**: 2-column table (`Concept | Remember`). Max 12 rows. Skip if the file is already table-heavy.
