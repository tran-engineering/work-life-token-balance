# Work Life Token Balance

## How leverage AI in development

![title](title.png)

### Khôi Tran - 02.07.2026

---

# This presentation

https://tran-engineering.github.io/work-life-token-balance/

![qrcode](qrcode.png)


---

## Disclaimer

This presentation is not meant to be **a definitive guide on AI** usage.

The tech is still in its infancy and **many best practices still change everyday**.

![disclaimer](disclaimer.png)

---

## Goal

The goal of this presentation is to provide **a practical introduction** to using LLMs for everyday tasks (mainly for developers).

**What's not the focus**: How things work under the hood, just the practical stuff. But we can always go on a tangent!

![devs](developer.png)

---

# How developers can interact with LLMs

![wrench](wrench.png)

---

## Levels of interaction

![levels](galaxy_brain.png)

---

## Web browser prompt

Everyone is familiar with this one:

- Easily accessible everywhere (e.g. also nice on the phone)
- No need to install anything
- Signing up for an account is optional
- Limited free usage

***

![browser](browser.png)

---

## Web browser prompt (2)

Usually gives quick validation for:

- Ideas, assumptions \
  *What is an LRU cache mostly used for?*
- Assessing feasibility \
  *Can I implement a 3D game in python?*
- Technology questions \
  *What libraries are there to work with geospatial data in ruby?*
- Design patterns \
  *What are the best practices for designing a REST API?*
- One time operations\
  *How do I setup Ollama on my local machine?*

---

## Web browser prompt (3)

Usually weaker for:

- Access to **surrounding code and context** (your repo, your local environment, your conventions)
- Cannot execute **commands, code / config files** locally, read log/error files
- **Context switching** between browser / CLI / IDE. the human is the copy/paste robot

---

## CLI and IDE Extensions

Many popular IDEs now have extensions that allow you to interact with LLMs directly from your editor.

![IDE ex](ide.png)

---

## General tips in CLI and IDE extensions

- Use `@<FILE>` to add a specific file as context
- Use `/` to trigger commands and skills (e.g. `/help`, `/clear`, `/review`)
- Attach images or screenshots directly into the chat (most tools support drag & drop or paste)
- Start a new conversation to reset context when switching tasks
- Be as specific as possible: "refactor this function to reduce nesting" beats "improve this"
- When the context window limit is reached, **compacting** will occur!

---

## VS Code

Usually via extensions:

- Claude
- OpenCode
- ...

Inline suggestions out-of-the-box (via GitHub Copilot).

***

![vscodeplug](vscode_plugin.png)

---

## VS Code specific tips

**Selected text in the editor** is automatically sent as context to the
LLM. If no lines are selected, the currently open file will be sent as context.

![exception](vscode_context.png)

---

## JetBrains

JetBrains has its own "AI Assistant" plugin, which supports:

- Junie (JetBrains AI)
- OpenAI Codex
- Claude Agent
- Others via ACP

***

![jbai](jetbrainsai.png)

---

## JetBrains AI Assistant specific stuff

- Selected text is not automatically put to context, also there is no keyboard shortcut to do so.

---

## Zed

Zed is a minimal rust based editor. With some AI features out of the box.

***

![zed](zed.png)

---

## Zed specific stuff

- Selected text in editor doesn't get put into the context of the LLM either
- But there's a dedicated shortcut reference the lines (`CTRL+Shift+>`)

---

## Plan vs. other modes

- **Plan mode** - the agent generates a plan of what to do before making any changes
- **Other modes** - the agent has some autonomous permissions

Other modes include:

- Ask before edits
- Edit automatically
- Auto mode
- Bypass all permissions (YOLO mode)

---

# What can LLM do with CLI / IDE integration?

![rmrf](rmrf.png)

---

## Developers can focus more time in the code base itself

- **Knows your codebase** — reads files, symbols, and project structure directly
- **Executes commands** — runs tests, builds, linters, and scripts on your behalf
- **Reads local context** — access logs, error traces, and config files without copy/pasting
- **Edits files directly** — applies changes inline instead of you having to transfer code manually
- **Stays in your flow** — no context switching between browser and editor
- **Works with private code** — nothing leaves your machine unless you choose it

---

## OMG! are there any guardrails?!

- **Permission prompts** — destructive or irreversible commands (e.g. `rm`, `git push`) require explicit user approval before running
- **Diff review** — file edits are shown as diffs so you can inspect and reject changes before accepting
- **No auto-push** — the agent won't push to remote or open PRs unless you ask it to
- **Scoped context** — the agent only reads files you've shared or that are in the working directory
- **You stay in control** — the agent proposes, you decide; it does not act autonomously by default

---

## Smaller code changes, refactors

`Extract the retry logic in api_client.rb into a separate module and add exponential backoff`

---

## Write tests

`Write unit tests for the UserService class covering the happy path and edge cases for invalid input`

---

## Explaining

`Explain what this file does and why the locking mechanism is needed here`

---

## Analysing

`Look at this stack trace and the relevant source files, and tell me what is causing the NullPointerException`

---

## Reviewing

`Review the changes on this branch and flag any bugs, security issues, or missing edge cases`

---

## Write documentation

`Generate a README for this project that explains what it does, how to run it, and how to contribute`

---

## Draw diagrams

`Create a Mermaid sequence diagram showing the flow of a user login request through the auth middleware`

---

## I'm too lazy to RTFM of git

- `Revert the last commit`
- `Commit and push`
- `Rebase this on develop branch and fix conflicts`

---

# Skills (Claude only)

---

## Skills

Skills are reusable, named prompts or workflows you invoke with a slash command (e.g. `/code-review`, `/security-review`) — they encode expert knowledge so you don't have to re-explain the same task every time. They are a **Claude Code-specific** feature; OpenCode does not currently support skills.

---

## How to define skills

Create a Markdown file — the filename becomes the slash command:

| Scope   | Path                                      | Invocation        |
|---------|-------------------------------------------|-------------------|
| Project | `.claude/commands/<skill-name>.md`        | `/skill-name`     |
| User    | `~/.claude/commands/<skill-name>.md`      | `/skill-name`     |

The file body is the prompt sent to the model when you invoke the skill. Use `$ARGUMENTS` to pass inline arguments (e.g. `/deploy production`).

---

## Out-of-the-box

| Skill | What it does |
| --- | --- |
| `/init` | Generate a `CLAUDE.md` for the current project |
| `/code-review` | Review the current diff for bugs and cleanups |
| `/security-review` | Security-focused review of pending changes |
| `/review` | Review a GitHub pull request by number |
| `/run` | Launch the project and verify a change in the running app |
| `/verify` | Confirm a fix works by exercising the app |
| `/simplify` | Refactor changed code for clarity and efficiency |

---

## Sample skill ideas

- `/standup` — summarise yesterday's git commits into a standup update
- `/ticket $ARGUMENTS` — create a Jira ticket from a short description
- `/changelog` — generate a changelog from commits since the last tag
- `/onboard` — explain the repo structure, stack, and how to run the project to a new joiner
- `/pr-description` — draft a pull request title and body from the current diff

---

# The next level: Tell the LLM how to work with **YOU**

---

## User instructions

Instructions that apply across **all your projects**:

| Tool        | Path                           |
|-------------|--------------------------------|
| Claude Code | `~/.claude/CLAUDE.md`          |
| OpenCode    | `~/.config/opencode/AGENTS.md` |

---

## Project specific instructions

Instructions scoped to a **specific project** (commit these to the repo):

| Tool        | Path                                   |
|-------------|----------------------------------------|
| Claude Code | `./CLAUDE.md` or `./.claude/CLAUDE.md` |
| OpenCode    | `./AGENTS.md`                          |

---

## Ideas for Instructions

- **Coding conventions** — naming style, file structure, preferred patterns
- **Tech stack** — language versions, frameworks, key libraries in use
- **How to run the project** — build, test, and lint commands
- **What to avoid** — deprecated APIs, banned patterns, files not to touch
- **Review checklist** — what to always check before committing (tests, docs, migrations)
- **Domain glossary** — project-specific terms and their meaning
- **Branch / PR conventions** — naming rules, commit message format
- **Personas** — tone and style when generating docs or commit messages

---

## ... the instructions don't write themselves, do they?

After a agentic session, you can tell it to update the instructions based on what you learned together!

---

## Advantages when using instructions

- **Fewer lookups** — the agent knows your stack upfront and won't ask how to run tests or where config lives
- **Less back-and-forth** — conventions are set once; you don't need to repeat them every session
- **Consistent output** — code style, naming, and structure stay uniform across all interactions
- **Shared with the team** — committing `CLAUDE.md` means every developer gets the same agent behaviour
- **Saves tokens** — no need to re-explain context in every prompt, keeping conversations focused
- **Faster onboarding** — new team members get project conventions explained by the agent for free

---

## Tips for writing instructions

- **Be specific** — vague instructions produce vague behavior; name files, functions, or patterns explicitly
- **Reference files directly** — use `@filename` or paste the path so the model can read current content rather than relying on your paraphrase of it
- **Include examples** — show a before/after or a sample output; one concrete example beats three sentences of description
- **State constraints, not just goals** — say what to *avoid* (e.g. "don't modify tests", "keep the existing API surface") as well as what to do
- **Separate concerns** — one instruction per bullet; bundled instructions get partially ignored

---

# Plug your LLM to the outside world: MCPs

---

## What is MCP?

MCP: Model Context Protocol

*Standardized Interface for LLMs to the outside world*

---

## MCP frameworks

| Language | Framework |
|----------|-----------|
| Python | [`fastmcp`](https://gofastmcp.com/) |
| Node.js | [`@modelcontextprotocol/sdk`](https://github.com/modelcontextprotocol/typescript-sdk) |
| Go | [`mark3labs/mcp-go`](https://github.com/mark3labs/mcp-go) |
| Rust | [`rmcp`](https://github.com/modelcontextprotocol/rust-sdk) |

---

## Contents of an MCP

- Set of tools
- Set of prompts

---

## Tools

A MCP tool is basically a description of a function and its parameters and its implementation.

```python
@mcp.tool(
    title="How Far Is It?",
    description=(
        "Calculate the straight-line (great-circle) distance between two places. "
        "Accepts any place name, city, address, or landmark. "
        "Returns the distance in both kilometres and miles."
    ),
    annotations=ToolAnnotations(
        readOnlyHint=True,
        destructiveHint=False,
        idempotentHint=True,
        openWorldHint=True,
    ),
)
def how_far_is_it(from_place: str, to_place: str) -> str:
    ...
```

---

## Prompts

```python
@mcp.prompt(
    title="Pirate mode",
    description="The LLM talks like a pirate.",
)
def pirate_mode() -> str:
    """Talk like a pirate."""
    return "Talk like a pirate and include a pirate-themed joke or pun in your response. Do not use any tools from this mcp."

```

---

# Nice, but what can it really do?

---

## Useful MCPs for devs

- Atlassian MCP
- GitHub MCP
- Gitlab MCP
- AWS MCP
- Context7 MCP

---

## Tips for working with MCPs

- Save tokens by disabling MCPs you don't need for the current task
- Prefer MCPs with **focused, well-named tools** — a bloated MCP wastes context on tool descriptions the model never uses
- **Read the tool list** before a session: knowing what's available helps you ask for exactly the right thing
- Chain MCPs together — e.g. fetch a Jira ticket, look up the related GitHub PR, then post a comment back, then play "We are the champions" on my computer

---

## DEMO

---

# Considerations for enterprisey setups

---


## Pricing

- Most tools charge per **token** (input + output) — costs add up fast with large context windows
- **Claude Code** uses a subscription model (no per-token billing for the end user)
- API access is cheapest but requires integration work; managed tools (Copilot, Cursor) bundle the cost
- Agentic loops can burn tokens quickly — a single session with many tool calls can cost several dollars

---

## Privacy

- By default, prompts sent to cloud LLMs **may be used for training** — check your provider's policy
- Enterprise/API tiers typically offer **zero data retention** and opt-out of training
- Avoid sending secrets, PII, or confidential business logic to public endpoints
- Self-hosted / local models (e.g. Ollama) keep everything on-premise — no data leaves your machine
- Check whether your company has a **DPA (Data Processing Agreement)** in place with the LLM provider

---

# Thanks
