# Lab 4 — Connect and Explore an MCP Server

**Lesson:** Module 4, *Using MCP Servers* (in the LearnPro app).
**Time:** about 30–45 minutes.
**Goal:** connect a ready-made server to a host, explore it by hand with the MCP Inspector, and judge it with the install checklist.

You will use the **Time** reference server. It offers two tools: `get_current_time` (input: `timezone`, an IANA name such as `Asia/Kolkata`) and `convert_time` (inputs: `source_timezone`, `time` as `HH:MM`, and `target_timezone`).

> Host menus and file locations change often. If a step below no longer matches your host, check its own MCP documentation.

## Step 0 — Check your setup

Run these in a terminal. Each should print a version number:

```
node --version
npx --version
uv --version
```

If `node` is missing, install Node.js. If `uv` is missing, install it from the link in the main README. The Inspector asks for a recent Node version and will tell you if yours is too old.

Try the server on its own first. It should start and wait quietly (press `Ctrl+C` to stop it):

```
uvx mcp-server-time
```

## Step 1 — Add the server to a host

Pick one host you use and add this entry (the format from the lesson):

```json
{
  "mcpServers": {
    "time": {
      "command": "uvx",
      "args": ["mcp-server-time"]
    }
  }
}
```

| Host | Where it goes | Note |
|---|---|---|
| Claude Desktop | `claude_desktop_config.json` (Settings > Developer > Edit Config) | quit the app completely and reopen it afterwards |
| Cursor | `.cursor/mcp.json` (project) or `~/.cursor/mcp.json` (all projects) | same format |
| VS Code | `.vscode/mcp.json` | use the key `servers` instead of `mcpServers`, and add `"type": "stdio"` to the entry |
| Claude Code | run `claude mcp add time -- uvx mcp-server-time` | writes the entry for you |

Restart or reload the host if it does not pick the server up. Hosts usually read the file only at start-up.

## Step 2 — Use it in a chat

Ask something that needs the tool, for example:

> What time is it in Tokyo right now?

Watch for the host asking permission to run a tool. Approve it once and note which tool it ran and what inputs it used.

## Step 3 — Explore it with the Inspector

Start the Inspector:

```
npx @modelcontextprotocol/inspector
```

In the page that opens, choose a local command (stdio) server, enter `uvx` as the command and `mcp-server-time` as the arguments, and connect.

Shortcut: put the server command after the Inspector command and it connects for you:

```
npx @modelcontextprotocol/inspector uvx mcp-server-time
```

Then:

1. List the tools. You should see `get_current_time` and `convert_time`.
2. Call `get_current_time` with `timezone` set to `Asia/Kolkata`.
3. Call `convert_time` with `source_timezone` `Europe/London`, `time` `09:00`, and `target_timezone` `Asia/Tokyo`.

What you should see: each result is a `content` list holding one text piece (the Module 3 shape), and the text is a small block of JSON. For the `convert_time` call, London 09:00 becomes **17:00** in Tokyo while London is on summer time (BST) and **18:00** when it is on winter time (GMT). The result also has `isError` set to `false`.

> The Time server speaks an older version of MCP that begins with a setup step. That is fine here: the Inspector and current hosts handle both versions.

## Step 4 — Run the install checklist

Copy `checklist.md` and fill it in for the Time server. Answer each of the five checks in a sentence.

## Done when

- [ ] The Time server is listed in your host and answered a question in a chat
- [ ] You called both tools by hand in the Inspector and saw a result
- [ ] Your `checklist.md` answers all five checks

## Troubleshooting

| Problem | Try |
|---|---|
| `uvx: command not found` | Install `uv`, then open a new terminal so it is on your path |
| Host shows no tools | Run the same command in the Inspector. If the Inspector works, the problem is your config file: check the JSON for a missing comma or bracket |
| Config changes have no effect | Fully restart the host, not just the chat |
| Inspector will not start | Update Node, then run the `npx` command again |
