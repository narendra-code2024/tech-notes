
---

This playbook provides a detailed technical reference for extending and controlling Claude Code via its five primary customization layers: Skills, Subagents, Hooks, and MCP.

---

## Skills — Reusable Workflows (Teach Claude Once)

> *From Introduction to Agent Skills (Skilljar): "You'll learn how to stop repeating yourself and start teaching Claude once."*

**What they are:** Markdown files (SKILL.md) that package reusable instructions, checklists, and procedures — invocable as slash commands or auto-triggered by Claude.

**The problem they solve:** Stop copy-pasting the same 200-word prompt every session. Write it once as a skill, call it forever.

**Key insight — Skills vs CLAUDE.md:**

| | CLAUDE.md | Skills |
|---|---|---|
| Loads | Always, on session start | Only when invoked / relevant |
| Best for | Permanent conventions & facts | Procedures, playbooks, workflows |
| Context cost | Always in window | Zero until used |

**Creating a skill:**
```bash
mkdir -p .claude/skills/pr-review
# Create .claude/skills/pr-review/SKILL.md
```

```markdown
---
name: pr-review
description: Review a pull request for code quality, security, and test coverage. Use when the user asks to review changes or a PR.
---

Review checklist:
1. Check for hardcoded secrets or API keys
2. Verify error handling is complete
3. Check test coverage for new logic
4. Flag performance concerns
5. Verify input validation
```

**Invocation**: Auto: Claude sees a task matching the description and loads it automatically
- Manual: `/pr-review`
- Arguments: `/pr-review src/auth/`

**Skill frontmatter options:**

| Field | Purpose |
|---|---|
| `name` | Display name → becomes `/slash-command` |
| `description` | When Claude auto-invokes this skill |
| `disable-model-invocation: true` | Prevent auto-load (for dangerous ops like deploy) |
| `user-invocable: false` | Hide from `/` menu (background knowledge only) |
| `allowed-tools` | Tools Claude can use without asking while skill runs |
| `context: fork` | Run skill in an isolated subagent |
| `paths` | Glob patterns limiting when skill auto-activates |

**Dynamic context injection**: run a shell command inside the skill body:
```markdown
## Current diff
!`git diff HEAD`

## Instructions
Summarise the changes above and flag anything risky.
```

**Skill directory structure:**
```
my-skill/
├── SKILL.md           # Main instructions (required)
├── template.md        # Template for Claude to fill in
├── examples/
│   └── sample.md      # Example output
└── scripts/
    └── validate.sh    # Script Claude can execute
```

**Where skills live (priority order):**
| Scope | Path |
|---|---|
| Enterprise (org-wide) | Managed settings |
| Personal (all projects) | `~/.claude/skills/<name>/SKILL.md` |
| Project (this repo only) | `.claude/skills/<name>/SKILL.md` |
| Plugin | `<plugin>/skills/<name>/SKILL.md` |

**Bundled skills (built-in):**
`/debug`, `/simplify`, `/batch`, `/loop`, `/claude-api`, `/run`, `/verify`

**Sharing skills with your team:** Commit `.claude/skills/` to your repo — every developer on the team gets the same workflows automatically.

---

## Subagents — Isolated Workers for Parallel Tasks

> *From Introduction to Subagents (Skilljar): "Learn how to use and create sub-agents in Claude Code to manage context, delegate tasks, and build specialized workflows that keep your main conversation clean and focused."*
> *From Claude Code 101 learning objectives: "Build custom subagents to delegate tasks and keep your main context clean."*

**What they are:** Specialized AI instances that run in their **own context window**, execute a task, and return only a summary to your main conversation. Verbose output — file searches, log dumps, test results — stays isolated.

**The problem they solve:** Big tasks pollute your main context. A subagent does the heavy lifting in its own window and reports back cleanly.

**Built-in subagents (auto-used by Claude):**

| Subagent | Model | Tools | Purpose |
|---|---|---|---|
| **Explore** | Haiku (fast, cheap) | Read-only | Codebase search & analysis |
| **Plan** | Inherits | Read-only | Research during Plan Mode |
| **General-purpose** | Inherits | All tools | Complex multi-step tasks |

**When to use subagents**: Task produces verbose output you don't need in main context (e.g. running the full test suite)
- You want to enforce tool restrictions (read-only review agent)
- Independent parallel research on separate topics
- Work is self-contained and can return a clean summary

**When NOT to use subagents**: Task needs frequent back-and-forth
- Multiple phases share heavy context with each other
- Latency is critical (subagents start fresh)

**Creating a subagent:**
```markdown
---
name: code-reviewer
description: Expert code review specialist. Reviews code for quality, security, and best practices. Use proactively after writing or modifying code.
tools: Read, Grep, Glob, Bash
disallowedTools: Write, Edit
model: sonnet
---

You are a senior code reviewer. When invoked:
1. Run `git diff` to see recent changes
2. Review modified files for: code clarity, error handling,
   no exposed secrets, input validation, test coverage
3. Report findings as: Critical / Warning / Suggestion
```

**Subagent frontmatter fields:**

| Field | Purpose |
|---|---|
| `tools` | Allowlist — only these tools available |
| `disallowedTools` | Denylist — inherit everything except these |
| `model` | `haiku`, `sonnet`, `opus`, or `inherit` |
| `permissionMode` | `default`, `auto`, `plan`, `bypassPermissions` |
| `skills` | Preload skills into subagent context |
| `mcpServers` | MCP servers scoped to this subagent |
| `hooks` | Hooks scoped to this subagent |
| `isolation: worktree` | Git branch isolation |
| `maxTurns` | Max agentic turns before stopping |

**Important:** Subagents do **not** inherit parent skills — preload them explicitly in frontmatter.

**Subagent scopes (priority order):**
| Scope | Path |
|---|---|
| Managed (org-wide) | Managed settings `.claude/agents/` |
| CLI flag | `--agents` JSON (session only) |
| Project | `.claude/agents/<name>.md` |
| Personal | `~/.claude/agents/<name>.md` |
| Plugin | `<plugin>/agents/<name>.md` |

**Parallel research pattern:**
```
Research the authentication, database, and API modules 
in parallel using separate subagents
```
- **Agent Teams (Advanced):** For massive parallel workloads (e.g., security audits), Claude can orchestrate multiple independent sessions that message each other directly to cross-check findings.


**Forked subagents (experimental):** Inherit full conversation history. Good when a subagent would need too much background context to start fresh.
```bash
CLAUDE_CODE_FORK_SUBAGENT=1
/fork draft unit tests for the parser changes
```

---

## Hooks — Deterministic System-Level Control

> *From Claude Code 101 learning objectives: "Write hooks for deterministic control over formatting, command blocking, and notifications."*
> *From Claude Code in Action curriculum: "Introducing hooks → Defining hooks → Implementing a hook → Gotchas around hooks → Useful hooks!"*

**What they are:** Event-driven scripts that fire at lifecycle points in the agentic loop. Unlike prompts (which depend on the model interpreting your instructions), hooks **execute deterministic code — they cannot hallucinate**.

**The problem they solve:** Without hooks, every safeguard depends on Claude "understanding" your rules. With hooks, you enforce rules at the **system level**: block before it runs, not after.

**Key lifecycle events:**

| Event | When | Can Block? |
|---|---|---|
| `UserPromptSubmit` | Before Claude sees your prompt | Yes |
| `PreToolUse` | Before any tool executes | Yes (primary security checkpoint) |
| `PermissionRequest` | When Claude asks for permission | Yes |
| `PostToolUse` | After tool completes | No (log / enforce linting) |
| `SessionStart` | When session begins | No (inject context) |
| `Stop` / `SubagentStop` | When Claude finishes | Yes (force continuation) |
| `Notification` | When Claude sends notification | No (route to Slack/TTS) |

**Exit code behaviour:**
| Exit Code | Meaning |
|---|---|
| `0` | Success — execution continues |
| `2` | Blocking error — action denied, error fed to Claude |
| `1` (other) | Non-blocking — warning shown, execution continues |

**Real-world hook examples:**
```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Write",
      "hooks": [{"type": "command", "command": "npm run lint"}]
    }],
    "PreToolUse": [{
      "matcher": "Bash",
      "hooks": [{"type": "command", "command": ".claude/hooks/block-dangerous.sh"}]
    }]
  }
}
```

**Common use cases**: Auto-lint every file Claude writes
- Block `rm -rf` before it runs
- Send Slack notification when Claude finishes a task
- Inject project context at session start
- Log every tool call for audit
- Require tests to pass before Claude can "stop"
- Enforce branch naming conventions

**Hook scopes:**
| Location | Scope |
|---|---|
| `~/.claude/settings.json` | All your projects |
| `.claude/settings.json` | This project (team-shared) |
| `.claude/settings.local.json` | This project, not shared |
| Subagent / skill frontmatter | Component lifetime |

---

## MCP (Model Context Protocol) — Connect External Tools

> *From Claude Code 101 learning objectives: "Connect external tools and data sources using MCP servers."*

**What it is:** Anthropic's open standard for connecting AI models to external tools and data sources through a unified interface. Sometimes called "USB-C for AI."

**The three MCP primitives:**

| Primitive | Controlled By | What It Does |
|---|---|---|
| **Tools** | Model | Actions: query DBs, make API calls, send messages |
| **Resources** | Application | Read-only data: config files, docs |
| **Prompts** | User/App | Pre-defined instruction templates |

**Without MCP:** Claude edits files and runs shell commands.
**With MCP:** Claude reads your JIRA tickets, queries your Postgres DB, checks Sentry, posts to Slack — all in a single workflow.

**Popular MCP servers:** GitHub, JIRA, Linear, Slack, Notion, Postgres, browser automation, and more. MCP servers are available in a growing ecosystem.

**Skills vs MCP (common confusion):**
> *"Skills are knowledge; MCP is action. A skill can instruct Claude to invoke MCP tools."*

---

## Plugins — Bundle & Distribute Everything

**What they are:** Plugins are **distribution packages** that bundle skills, subagents, hooks, and MCP server configs into a single installable unit. Where skills and subagents are individual building blocks you write yourself, a plugin is a complete, shareable configuration you install once and use everywhere.

**The problem they solve:** Instead of manually copying `.claude/skills/` and `.claude/agents/` files across every project or team member's machine, you package them into a plugin that installs in one step.

**What a plugin can contain:**

| Component | What it contributes |
|---|---|
| **Skills** | Available as `/plugin-name:skill-name` commands |
| **Subagents** | Available in `/agents` alongside your custom ones |
| **Hooks** | Fire automatically in any project where the plugin is enabled |
| **MCP server config** | Pre-configured MCP connections bundled in |

**Plugin skill namespace:** `plugin-name:skill-name` — prevents conflicts with your own skills.

> **Security note:** Plugin subagents cannot define `hooks`, `mcpServers`, or `permissionMode` in their frontmatter — those fields are stripped for safety. If you need them, copy the agent file into `.claude/agents/` locally.

**Where plugins live:**
```
<plugin>/
├── skills/
│   └── <skill-name>/SKILL.md
├── agents/
│   └── <agent-name>.md
└── plugin.json              # Plugin manifest
```

**Installing a plugin:**
```bash
/plugins install <plugin-name-or-path>
```

**Discovering plugins:**
```bash
/plugins discover     # Browse available plugins
```

**Team use case:** Your team creates a company plugin that bundles:
- A `/pr-review` skill pre-loaded with your coding standards
- A `security-reviewer` subagent
- A `PostToolUse` lint hook
- Your internal JIRA MCP server config

Every new developer installs the plugin once and gets the entire team's workflow setup instantly — no manual file copying, no onboarding friction.

**Plugins vs Skills vs Subagents — when to use each:**

| | Skills | Subagents | Plugins |
|---|---|---|---|
| **Unit of reuse** | Single workflow/procedure | Single specialized worker | Bundle of all of the above |
| **Scope** | One behaviour | One agent persona | Complete team configuration |
| **Share via** | Commit to repo | Commit to repo | Install as package |
| **Best for** | Repeatable tasks | Parallel/isolated work | Team/org standardisation |
