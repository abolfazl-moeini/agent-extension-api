# Creating Cursor Plugins

Source: [cursor.com/docs/plugins](https://cursor.com/docs/plugins)

## Overview

A Cursor plugin is a directory with a `.cursor-plugin/plugin.json` manifest and optional components: rules, skills, agents, commands, MCP servers, and hooks.

## Scaffold

Start from the [plugin template](https://github.com/cursor/plugin-template) or create from scratch:

```
my-plugin/
├── .cursor-plugin/
│   └── plugin.json
├── rules/
│   └── coding-standards.mdc
├── skills/
│   └── code-reviewer/
│       └── SKILL.md
├── agents/
│   └── security-reviewer.md
├── commands/
│   └── deploy.md
├── hooks/
│   └── workspace-open.sh
└── mcp.json
```

## Manifest

`plugin.json` requires only `name`. All other fields are optional.

```json
{
  "name": "my-plugin",
  "description": "Custom development tools for my team",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "email": "you@example.com"
  }
}
```

Components are auto-discovered from default directories. Override paths in the manifest if needed. See `reference.md` for the full schema.

## Adding Components

### Rules

`.mdc` files in `rules/` with frontmatter:

```markdown
---
description: React component patterns for this project
globs: "**/*.tsx"
alwaysApply: false
---

Use functional components with hooks. Prefer named exports.
```

### Skills

Directories with `SKILL.md` in `skills/`. Follow the Agent Skills standard (`standards/agent-skills.md`).

### MCP Servers

`mcp.json` at plugin root:

```json
{
  "mcpServers": {
    "my-api": {
      "command": "npx",
      "args": ["-y", "my-mcp-server"],
      "env": {
        "API_KEY": "${env:MY_API_KEY}"
      }
    }
  }
}
```

### Hooks

Shell scripts in `hooks/` that respond to events. Use the `workspaceOpen` hook to return plugin paths dynamically.

## Local Testing

1. Create `~/.cursor/plugins/local/my-plugin/`
2. Copy plugin files (or symlink):
   ```bash
   ln -s /path/to/my-plugin ~/.cursor/plugins/local/my-plugin
   ```
3. Restart Cursor or run **Developer: Reload Window**
4. Open **Customize** sidebar to verify rules, skills, and MCP servers load

## Publishing

1. Ensure plugin is open source (marketplace requirement)
2. Submit at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish)
3. Every plugin and update is manually reviewed

For multi-plugin repos, add `.cursor-plugin/marketplace.json`.

## Team Marketplaces

Teams and Enterprise plans support private marketplaces:

1. Dashboard → Settings → Plugins → Add Marketplace
2. Import from GitHub repo (e.g. [team marketplace template](https://github.com/fieldsphere/cursor-team-marketplace-template))
3. Set distribution groups (required vs optional)
4. Enable Auto Refresh for automatic updates

## MCP Install Deeplinks

Share server configs via install links:

```
cursor://anysphere.cursor-deeplink/mcp/install?name=$NAME&config=$BASE64_ENCODED_CONFIG
```

See [MCP install links](https://cursor.com/docs/mcp/install-links) for generation details.