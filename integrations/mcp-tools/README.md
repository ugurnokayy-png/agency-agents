# MCP Tools Integration

> Extend any agent in The Agency with a standard toolkit of MCP servers for
> browsing, file management, search, cross-tool connections, and quality gates.

## What It Does

Agents work best when they can act on the real world instead of just
producing text. Wiring in a small set of MCP servers gives every agent:

- **Browser (Puppeteer MCP)** — opens and safely drives live websites on
  the agent's behalf, so it can check a deployed page, scrape a source, or
  verify a UI change.
- **File Manager (Filesystem MCP)** — organizes project folders and files
  and keeps the project from turning into a mess as agents create output.
- **Search Tool (Brave Search / Fetch)** — finds information the agent
  doesn't already have, quickly.
- **Connection Layer (Smithery / n8n integrations)** — lets the different
  tools an agent uses talk to each other instead of working in isolation.
- **Quality Gate (Git / GitHub MCP)** — checks a change for errors and
  risk before it's applied, using version control as the safety net.

## Setup

Add the servers you need to your MCP client config (Claude Code, Cursor,
etc.):

```json
{
  "mcpServers": {
    "puppeteer": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-puppeteer"]
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/project"]
    },
    "brave-search": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-brave-search"],
      "env": { "BRAVE_API_KEY": "your-api-key" }
    },
    "fetch": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-fetch"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": { "GITHUB_PERSONAL_ACCESS_TOKEN": "your-token" }
    }
  }
}
```

The Connection Layer (Smithery, n8n) isn't a single server — it's whatever
automation platform you use to route data between the tools above and the
rest of your stack. Check the [MCP ecosystem](https://modelcontextprotocol.io)
and [Smithery registry](https://smithery.ai) for hosted or self-run options.

## How to Use These Tools From an Agent

Any agent's prompt can reference these tools directly — no code changes
required. Add a short note describing which tools it has and when to reach
for them, for example:

```markdown
## Available Tools

- Use the browser tool to verify live pages before reporting a UI fix as done.
- Use the filesystem tool to keep generated files organized under the
  project's existing directory structure, not scattered at the root.
- Use search before guessing at facts you don't already know.
- Before finishing a change, use the Git/GitHub tools to check the diff
  for risk and confirm it's safe to apply.
```

## Tips

- **Scope the filesystem server** to the project directory, not the whole
  home directory — agents should only touch what they're working on.
- **Treat the quality gate as non-optional**: an agent with Git/GitHub
  access should check a diff before applying it, the same way a human
  reviewer would.
- **Least privilege for search and browser tools**: give read-only or
  scoped API keys where the provider supports it.
