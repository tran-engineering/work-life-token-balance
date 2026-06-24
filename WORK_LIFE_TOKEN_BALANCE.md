# Work Life Token Balance

## How leverage AI in development

## Khôi Tran - 02.07.2026

---

## Disclaimer

This presentation is not meant to be a definitive guide on AI usage.

The tech is still in its infancy, and the possiblities are endless.

---

## Goal

The goal of this presentation is to provide a practical introduction to using LLMs mainly for developers
for everyday tasks.

---

## Agenda

1. How can developers interact with LLMs?

---

# How to interact with LLMs

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

---

## Web browser prompt (2)

Usually gives quick validation for:

- Ideas, assumptions (*What is an LRU cache mostly used for?*)
- Assessing feasibility (*Can I implement a 3D game in python?*)
- Technology questions (*What libraries are there to work with geospatial data in ruby?*)
- Design patterns (*What are the best practices for designing a REST API?*)
- One time operations (*How do I setup Ollama on my local machine?*)

---

## Web browser prompt (3)

Usually weaker for:

- Feedback/Tips on code (requires you to copy/paste code from the browser, doesn't know your codebase, conventions, etc.)
- Cannot access private information (e.g. your local environment, private repositories)
- Cannot execute commands, code locally, read log files

---

## CLI and IDE Extensions

Many popular IDEs now have extensions that allow you to interact with LLMs directly from your editor.

---

## General conventions in CLI and IDE extensions

- Use `@<FILE>` to add a specific file as context
- Use `/` to trigger slash commands (e.g. `/help`, `/clear`, `/review`)
- Attach images or screenshots directly into the chat (most tools support drag & drop or paste)
- Start a new conversation to reset context when switching tasks
- Be as specific as possible: "refactor this function to reduce nesting" beats "improve this"

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

# What can LLM do with CLI / IDE integration?

---

## The vibe coder: Build everything from scratch

TODO: Example

---

## Smaller code changes, refactors

TODO: Example

---

## Explaining

TODO: Explain some difficult to understand code

---

## Analysing

TODO: Analyse exception cases if it makes sense

---

## Reviewing

TODO: Example Review everything / branch / pr

---

## Write documentation

TODO: Example write documentation

---

## Draw diagrams

TODO: Example

---

# The next level: Tell the LLM your conventions

---

# Plug your LLM to the outside world: MCPs

---

