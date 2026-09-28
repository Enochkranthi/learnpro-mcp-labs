# LearnPro MCP Labs

Hands-on labs for the **Model Context Protocol (MCP)** course in the LearnPro app. Each lab matches a module in the course and has its own folder under `labs/`.

## How it works

1. Read the module in the app. It tells you when a lab is waiting.
2. Open the lab's folder here (`labs/moduleNN`) and follow its README.
3. Each lab starts from the previous lab's finished state, so skipping one never blocks the next.

## Labs

| Lab | Module | What you do |
|---|---|---|
| [module04](labs/module04/README.md) | Using MCP Servers | Connect a reference server to a host, explore it with the Inspector, run the install checklist |

More labs are added as the course modules are published. From Module 5 on, you build **HelpDesk MCP**, one server that grows across the course.

## What you need

- A laptop (macOS, Windows or Linux)
- A host app with MCP support (Claude Desktop, Cursor, VS Code, or Claude Code)
- Node.js (a recent version) and [`uv`](https://docs.astral.sh/uv/)
- Python 3.12 or newer, from Module 5 on

## Status

The `labs` command-line helper (`labs doctor`, `labs check`, `labs hint`) and the in-app lab card are planned but not built yet. Until then, each lab has a written checklist you tick off yourself.
