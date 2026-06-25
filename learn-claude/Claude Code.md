# Claude Code

From Everyday AI to Agentic Engineering.

---

## Introduction to Claude

Claude is more than a chatbot, it's an AI assistant designed to be your thinking partner, built to be **helpful, harmless, and honest**. Unlike general chatbots, Claude emphasises safety and honesty through Anthropic's **Constitutional AI** approach.

### Core Capabilities
- **Massive Context:** 200K+ tokens (500+ pages) standard; up to **1M tokens** on the latest Opus and Sonnet models for processing entire repositories or documentation libraries.
- **Deep Reasoning:** Hybrid models (Sonnet/Opus 4.x) offer **Extended Thinking** for complex logic, mathematical problems, and step-by-step planning.
- **Steerable & Collaborative:** Highly adaptable to specific tones and behaviors; designed to be a "thought partner" that can augment and automate complex workflows.
- **Helpful, Harmless, Honest:** Trained via **Constitutional AI** to align with human values, refuse illegal or unethical requests, avoid toxic or discriminatory output, and operate transparently.

---

## Ways to Access Claude

| Surface | Best For |
|---|---|
| **Claude.ai** (Web / Mobile) | General chat, research, **Artifacts**, and **Learning Mode**. |
| **Claude Desktop** | All web features + **Cowork** (screen-aware automation). |
| **Claude Code** (CLI / IDE) | Agentic engineering and direct local file manipulation. |
| **Slack Integration** | **Workspace search** across channels, DMs, and shared files. |
| **Excel / PowerPoint / Word** | Formula debugging, template-aware slide creation, and document drafting. |
| **Claude API** | Building custom agentic tools and enterprise scale. |

---

## Claude Code

Claude Code is an agentic coding tool: it understands your codebase, edits files, runs commands, and modifies files. While designed for developers, it is capable of any complex file manipulation on your system.

It is available via the terminal, VS Code/JetBrains extensions, and the Claude Desktop app.

### Installing Claude Code

**Prerequisites**: Node.js installed (**Latest LTS recommended**)
- A Claude account: Pro, Max, Team, or Enterprise (or an API key)

**Option 1 (Terminal / CLI):** Install globally via npm, then launch from any project directory.
```bash
npm install -g @anthropic-ai/claude-code
claude
```

**Option 2 (IDE Extension):** Install the **Claude Code** extension directly inside your editor for inline diffs and selection-aware context.
- **VS Code** (and forks like Cursor / Windsurf): install from the Marketplace, or run `claude` once in the integrated terminal to auto-install.
- **JetBrains** (IntelliJ, PyCharm, WebStorm, etc.): install the plugin from Settings → Plugins, then restart the IDE.

---

## The Agentic Loop

An **AI agent** is software that pursues a goal by running a language model in a loop: it takes real actions through tools (reading files, running commands, calling services) and uses each result to decide the next step. This is what sets Claude Code apart from a typical chat application, it operates through an **agentic loop**:

1. **Prompt:** You enter a prompt into the terminal.
2. **Gather Context:** Claude interacts with the model to identify necessary files and context.
3. **Take Action:** It executes a tool call (e.g., editing a file or running a command).
4. **Verify Results:** It determines if the action achieved the prompt's goal.
5. **Finish or Loop:** If successful, it finishes. If not, it loops back to step 2 and tries again until the results are verifiable.

```
                  +-----------------------------------------------------------+
                  |                       Agentic Loop                        |
                  |                                                           |
+-------------+   |   +----------+       +-------------+       +------------+ |   +----------+
| Your prompt |------>|  Gather  | ----> | Take action | ----> |   Verify   |---->|   Done   |
+-------------+   |   | context  |       |             |       |  results   | |   +----------+
                  |   +----------+       +-------------+       +------------+ |
                  |        ^                                          |       |
                  |        +------------------------------------------+       |
                  +-----------------------------------------------------------+
                                          ^
                                          |
                        +------------------------------------+
                        | You interrupt, steer or add context |
                        +------------------------------------+
```

> **Note**: Press `Esc` to interrupt a run and steer, the feedback point shown in the loop above.

---

## Permission Modes, Slash Commands & Models

### Permission Modes

You control Claude's autonomy through three primary behaviors, cycled with **`Shift + Tab`**:

| Mode | Behavior |
|---|---|
| **Default** | Asks for explicit permission before editing a file or running a shell command. |
| **Auto-accept** | Automatically edits files; still asks for permission before running commands. |
| **Plan Mode** | Uses read-only tools to build a plan of action *before* any work begins. |
### Slash Commands & Models
- **Slash commands:** Typed in the prompt (e.g., `/init`, `/context`, `/clear`), these trigger built-in actions, custom skills, and plugins. Type `/` to browse the full list.
- **Model selection:** Use `/model` to switch between **Opus** (deepest reasoning), **Sonnet** (balanced default), and **Haiku** (fast, cheap). Match the model to the task to control cost and speed.

---

## Context Management

Context is Claude's working memory. Every file it reads, every command it runs, every message you send, it all takes up space in the context window. When you approach the limit, Claude automatically compacts (summarizes) the session to free up space, though some detail can be lost in the process.

| Command | Action | When to Use Which |
|---|---|---|
| **`/context`** | View state | To check your context size and see exactly what is consuming space. |
| **`/compact`** | Manual summary | When low on space mid-feature; run proactively (~70% usage) to keep logic sharp. |
| **`/clear`** | Full reset | When starting a **new feature** to prevent old context from introducing bias. |

---

## CLAUDE.md

**The Problem:** Without a `CLAUDE.md`, Claude starts fresh every time you open a **new session**: re-exploring the codebase and making assumptions that lead to constant course-corrections.

**The Solution:** `CLAUDE.md` acts as a persistent **onboarding script**. It is automatically loaded to every session so Claude already knows your stack and rules.

| Feature | Description |
|---|---|
| **Hierarchy** | **User-level** (personal preferences) vs **Project-level** (team conventions). |
| **The @ Symbol** | Use `@file_path` inside `CLAUDE.md` to reference other docs in project. |
| **Initialization** | Run **`/init`** once you've identified the guidance you keep repeating. |

CLAUDE.md Best Practices:

- **The 200 Lines Rule:** Keep `CLAUDE.md` under 200 lines. A shorter, denser file has higher signal-to-noise and leads to better agent behavior.
- **Save Corrections:** If you find yourself correcting Claude repeatedly, explicitly ask it to update `CLAUDE.md`.
- **Start Without One:** Let the project reveal where the model fails first so your file stays focused; when you're ready, run `/init` to generate one.

---

## Customizing Claude Code

Claude Code is a **programmable platform**. A few core systems let you control, extend, and automate its behavior:

### Skills: Reusable Workflows
Markdown files (`SKILL.md`) that package instructions and procedures.
- **Problem:** Repeating the same 200-word prompt every session.
- **Solution:** Teach Claude once; call forever via `/skill-name`.
- **Scope:** Project skills live in `<project>/.claude/skills/` (commit them to share with your team); personal skills live in `~/.claude/skills/` and apply across all your projects.

### Subagents: Isolated Workers
Specialized AI instances that run in their **own context window**.
- **Use Case:** Delegate verbose tasks (like log analysis or running full test suites) to keep your primary context clean.
- **Hierarchy:** Inherit parent permissions but **not** parent skills (must be preloaded explicitly).
- **Create one:** Run `/agents` for a guided flow, pick the scope (project vs personal), describe the purpose, and Claude generates the config. Saved as a Markdown file with YAML frontmatter.

### Hooks: Deterministic Control
Scripts that fire at lifecycle points (e.g., `PreToolUse`, `Stop`).
- **The Difference:** Unlike prompts, hooks execute **real code** and cannot hallucinate.
- **Example:** A `PostToolUse` hook that runs `npm run lint` or Prettier after every file edit.
- **Configure:** Defined in `settings.json` via the `/hooks` command. Key events: `PreToolUse`, `PostToolUse`, `UserPromptSubmit`, `Stop`, `Notification`.

### MCP (Model Context Protocol): External Tools & Data
"USB-C for AI", connecting Claude to external data and tools.
1. **Tools:** Actions (Query DB, post to Slack).
2. **Resources:** Data (Read config files, docs).
3. **Prompts:** Templates (Pre-defined instruction sets).

Add a server with one command, then manage them with `/mcp`:
```bash
claude mcp add --transport http github https://api.githubcopilot.com/mcp/
```

---

## Automate Workflows

Claude Code integrates with your entire development toolchain via MCP and hooks. These are the highest-value automation patterns:

### Ticket Creation & Documentation (JIRA / Confluence)

**How:** Claude uses MCP to bridge the gap between "Requirements" and "Implementation." It can analyze technical debt or roadmap specs and autonomously generate a backlog.

**High-Fidelity Example (Strategic Breakdown):**
> *"Read our product spec in @docs/v2-roadmap.md. Compare it against the current /auth implementation. For every missing feature or required change, create a JIRA story in the 'V2 Launch' project. Include implementation notes for each story."*

### PR & Code Reviews

**How:** Claude analyzes the diff against your repository conventions (`CLAUDE.md`). Use the built-in commands rather than rolling your own:
- **`/review`**: reviews a pull request.
- **`/code-review`**: reviews the current diff for correctness bugs and cleanups.
- **`/security-review`**: audits pending changes for security issues.

**Expert Tip:** These run an isolated **Subagent** on the **git diff** first, keeping the review focused and preventing Claude from wasting context on unrelated files. Can also be automated via a `git push` hook.

### Fix Review Comments

**How:** Point Claude at open PR comments. It maps the conversational feedback directly to file line numbers and applies surgical fixes.

**Prompt Example:**
> *"Fix all review comments on PR #142. Do not refactor or change any code not specifically mentioned in the comments."*

---

## Getting Better Results

### Anatomy of an Effective Prompt

Talk to Claude like a capable coworker: naturally, concisely, conversationally. A strong prompt carries three things, and the tactics below are just ways of sharpening each one:

- **Context (set the stage):** Your role, your objective, and the background Claude needs.
- **Task (the action):** Exactly what to do, write, analyze, refactor, or build.
- **Rules (the guardrails):** Style, tone, format, constraints, and any example to mirror.

**Example:**
> *"You’re an expert backend engineer skilled in Node, Express and Redis* (context). *Add rate limiting to the /login route* (task). *Reuse the existing Redis client, return HTTP 429 on limit, and leave unrelated routes untouched* (rules)."

### Techniques

- **Plan Mode First:** Don't jump straight to code. Let Claude explore and propose a plan you review before it writes anything, the cheapest point to catch a wrong approach and avoid course-correction later.
- **Explicit Mapping:** Use exact file paths and line numbers, e.g. *"Refactor lines 10-30 in src/auth.ts"*.
- **Negative Prompts:** Tell Claude what **NOT** to do, e.g. *"Don't add logs. Don't use external libraries."*
- **Trust but Check:** For high-stakes facts, ask Claude to cite sources or enable web search, then confirm independently.

---

## Security

Claude Code runs in developers' terminals with **the same permissions as the user**: reading files, executing commands, and accessing production systems. This is not a chatbot, which is why permissions, deny rules, and managed settings matter.

### Risks & Mitigations

| Category | Risk | Mitigation |
| :--- | :--- | :--- |
| **System Integrity** | Malicious prompts run destructive commands (`rm -rf`, data exfil). | Use **`PreToolUse` Hooks** to block dangerous commands. |
| **Data Leakage** | Claude reads `.env`, SSH keys, or AWS credentials. | Set **Deny Rules** on sensitive paths in `settings.json`. |
| **Supply Chain** | Rogue updates to an approved MCP server. | **Version-pin** all MCP servers and audit before approval. |
| **Injection** | Malicious instructions embedded in files Claude reads. | Use **Isolated Subagents** for processing untrusted content. |

### Managed Settings

Managed settings allow organizations to enforce safety rules that developers cannot override via `--dangerously-skip-permissions`.

Block the highest-risk commands and sensitive paths via managed `deny` rules:
```json
"deny": [
  "Bash(curl:*)", "Bash(wget:*)",
  "Read(**/.env)", "Read(**/.ssh/**)",
  "Read(**/credentials/**)"
]
```

---

## Resources

Community registries for discovering skills and MCP servers:

- **[skills.sh](https://skills.sh)**: Community registry for **Agent Skills** (reusable instruction sets).
- **[smithery.ai](https://smithery.ai)**: Registry for discovering and installing **MCP Servers**.
- **[mcp-get.com](https://mcp-get.com)**: A curated directory for the **Model Context Protocol** ecosystem.

Official Anthropic Academy courses:

- **[Claude 101](https://anthropic.skilljar.com/claude-101)**: The foundation for all users.
- **[Claude Code 101](https://anthropic.skilljar.com/claude-code-101)**: Essential for agentic engineering.
- **[Introduction to Agent Skills](https://anthropic.skilljar.com/introduction-to-agent-skills)**: Master the art of writing `SKILL.md`.
- **[Introduction to Subagents](https://anthropic.skilljar.com/introduction-to-subagents)**: Managing complex, parallel workloads.
