# Orbit: Shared AI Memory (MCP server)

Orbit gives Claude, GitHub Copilot and your other AI tools one shared memory. Tell one AI your writing style, a project decision or a constraint, and the next AI you open can recall it. You choose what each AI can read and save in the free Orbit iPhone app.

This repository describes Orbit's hosted MCP server. The server is remote and fully managed, so there is nothing to install or run.

- Server URL: `https://api.orbit.cloudytuesdays.com/mcp`
- Transport: Streamable HTTP
- Auth: OAuth 2.1 (Client ID Metadata Documents and Dynamic Client Registration), scope `memory`
- Registry name: `com.cloudytuesdays/orbit`
- Docs: https://orbit.cloudytuesdays.com/docs/
- Privacy: https://orbit.cloudytuesdays.com/privacy/
- Support: help@cloudytuesdays.com

## What it does

| Tool | What it does | Access |
|---|---|---|
| `recall` | Returns saved memories relevant to the task, from the topics this connection may read | Read |
| `brief` | Builds a continuation brief for a project: decisions, constraints, rejected approaches, current state, next steps, preferences | Read |
| `capabilities` | Shows this connection's workspace, allowed operations, topics and limits | Read |
| `remember` | Saves facts the user stated, with the user's own words kept as evidence | Write |
| `update_memory` | Replaces the value of one memory the user corrected; the earlier version stays in history | Write |
| `forget` | Moves one memory to Recently deleted, restorable for 30 days (permission off by default) | Write |

Every memory is treated as data, never as instructions. Orbit skips anything that looks like a password, key, ID or card number.

## Configure

You need the free Orbit iPhone app with Sign in with Apple.

**VS Code / GitHub Copilot** (`.vscode/mcp.json`):

```json
{
  "servers": {
    "orbit": {
      "type": "http",
      "url": "https://api.orbit.cloudytuesdays.com/mcp"
    }
  }
}
```

**Claude:** Settings > Connectors > Add custom connector, then paste `https://api.orbit.cloudytuesdays.com/mcp`.

**Any MCP client with remote HTTP support:** add the server URL above. The client opens a browser sign-in on first use; approve it in the Orbit app, pick a workspace and the topics this AI may read and save.

## Use

Try prompts like:

- "Check Orbit for my writing preferences, then draft the intro."
- "Give me an Orbit brief for the website redesign and pick up where I left off."
- "Remember that we decided to ship the beta on Friday."
- "That's out of date: update the Orbit memory about my deadline to December 5."
- "What can you see in my Orbit?"

## Permissions and privacy

- Each AI connection gets one workspace and its own read and save topics. Health, Finance and Relationships start off.
- Deleting memories stays off until you turn it on.
- Permission changes apply on the next request; disconnect any AI at any time in the app.
- Review, correct, restore, export or delete every memory in the app.

## Plans

The free plan connects 2 AIs and holds 150 memories. Orbit Pro ($4.99 a month, or $39.99 a year with a 7-day free trial) connects up to 10 AIs.

---

Made by Cloudy Tuesdays. The server source is private; this repository holds its public description.
