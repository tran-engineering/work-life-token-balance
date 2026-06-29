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

This presentation is not meant to be a definitive guide on AI usage.

The tech is still in its infancy, and the possibilities are endless.

![disclaimer](disclaimer.png)

---

## Goal

The goal of this presentation is to provide a practical introduction to using LLMs for everyday tasks (mainly for developers).

![devs](developer.png)

---

# How to interact with LLMs

![wrench](wrench.png)

---

## Levels of interaction

![levels](galaxy_brain.png)

---

## Web browser prompt

Everyone is familiar with this one:

- Easily accessible everywhere (e.g. also nice on the phone)
- No need to install anything
- No need to sign up for an account
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

- Feedback/Tips on code (requires you to copy/paste code from the browser, doesn't know your codebase, conventions, etc.)
- Cannot access private information (e.g. your local environment, private repositories)
- Cannot execute commands, code locally, read log/error files

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

---

## VS Code specific tips

Selected text in the editor is usually automatically sent as context to the
LLM. If no lines are selected, the currently open file will be sent as context.

![exception](vscode_context.png)

---

## JetBrains

JetBrains has its own "AI Assistant" Plugin, which supports:

- Junie (JetBrains AI)
- OpenAI Codex
- Claude Agent
- Others via ACP

---

## JetBrains AI Assistant specific stuff

- Selected text is not automatically put to context, also there is no keyboard shortcut to do so.

---

## Zed

Zed is a minimal rust based editor. With a penchant to AI features.

---

## Zed specific stuff

- Selected text in editor doesn't get put into the context of the LLM either
- But there's a dedicated shortcut reference the lines (`CTRL+Shift+>`)

---

## Plan vs. Build mode

- **Plan mode** — the agent generates a plan of what to do before making any changes
- **Build mode** — the agent applies changes directly to the codebase without generating a plan first

---

# What can LLM do with CLI / IDE integration?

![rmrf](rmrf.png)

---

## Developers can focus more on coding

- **Knows your codebase** — reads files, symbols, and project structure directly
- **Executes commands** — runs tests, builds, linters, and scripts on your behalf
- **Reads local context** — access logs, error traces, and config files without copy/pasting
- **Edits files directly** — applies changes inline instead of you having to transfer code manually
- **Stays in your flow** — no context switching between browser and editor
- **Works with private code** — nothing leaves your machine unless you choose it

---

## OMG are there any guardrails?!

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

# The next level: Tell the LLM your conventions

---

## User files

Instructions that apply across **all your projects**:

| Tool        | Path                           |
|-------------|--------------------------------|
| Claude Code | `~/.claude/CLAUDE.md`          |
| OpenCode    | `~/.config/opencode/AGENTS.md` |

---

## Project files

Instructions scoped to a **specific project** (commit these to the repo):

| Tool        | Path                               |
|-------------|------------------------------------|
| Claude Code | `CLAUDE.md` or `.claude/CLAUDE.md` |
| OpenCode    | `AGENTS.md`                        |

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

- Collection of tools
- Collection of prompts

---

## Tools

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
