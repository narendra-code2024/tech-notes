---
name: note-reviewer
description: Audits and optimizes a technical note against the project's official Technical Note Standards, covering structure, formatting, pedagogical ordering, high-yield filtering, redundancy/density, and Q&A and cheat-sheet quality.
---

# Note Reviewer Skill

Audit a technical note for full compliance with the canonical standards in @.agents/rules/standards.md.

## How to Audit
Every review has two concerns, both required: **compliance** and **optimization**.

**Compliance**: read @.agents/rules/standards.md and check the note against every section systematically, treating each rule as a checklist item and skipping none.

**Optimization**: run a redundancy / low-yield / density pass across the *whole* note, even where no rule is strictly broken. Cover everything, not just prose: body, structure, tables, Q&A, Cheat Sheet, and code blocks read line by line. Actively apply the standards' content rules (**High-Yield Filtering**, the **3+ Exp Dev Standard**, **Conciseness & Information Density**, **Intra-note redundancy**, and **Comment Redundancy Elimination**), flagging anything they cover for removal or tightening. *Crucially, optimization means compacting and refining existing content, not blindly appending new standalone sections or separate code blocks that bloat the file. Proactively seek to consolidate adjacent content and explanations to maximize information density.*

### Proactive Design & Restructuring Decisions
Do not wait for the user to explicitly suggest structural or logical changes. As an expert reviewer, you must proactively:
1. **Consolidate Thin Sections**: Identify and merge thin or minor `##` sections under broader, logical parent sections or flatten them.
2. **Remove Redundant Content**: Locate and remove sections, tables, or lists that repeat information already covered in primary comparison tables or cheat sheets.
3. **Verify Code Semantics**: Ensure code blocks are compile-ready and contain no duplicate outer class declarations in the same block.
4. **Upgrade Q&A & Cheat Sheets**: Replace elementary textbook questions with high-yield JVM mechanics, compiler artifacts (like `this$0`), garbage collection impacts, and modern features (like JEP 181 Nestmates).
5. **Consolidate Sibling Code Blocks**: Merge separate code blocks of related sibling subtopics into a single, unified, well-commented code block to eliminate import and class declaration overhead.

## Output Format
1. **Violations & Optimizations Report**: List each violation (with quotes and rule name) and suggested optimization.
2. **Refactored Note**: Provide the complete, fully refactored, and formatted note in a code fence or as a linked artifact. This allows the user to review the entire corrected note in a single step and approve the update.

If the note has no violations and no optimization opportunities, respond with "✅ Note matches all Project Standards."
