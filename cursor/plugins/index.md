# Cursor Plugins

Source: [cursor.com/docs/plugins](https://cursor.com/docs/plugins)

Plugins package rules, skills, agents, commands, MCP servers, and hooks into distributable bundles.

## What Plugins Contain

| Component | Description | Location |
|-----------|-------------|----------|
| **Rules** | Persistent AI guidance (`.mdc` files) | `rules/` |
| **Skills** | Agent capabilities (`SKILL.md`) | `skills/` |
| **Agents** | Custom agent configurations | `agents/` |
| **Commands** | Agent-executable commands | `commands/` |
| **MCP Servers** | External tool integrations | `mcp.json` |
| **Hooks** | Event automation scripts | `hooks/` |

## Quick Start

```bash
# 1. Create plugin directory
mkdir -p my-plugin/.cursor-plugin

# 2. Add manifest
cat > my-plugin/.cursor-plugin/plugin.json << 'EOF'
{
  "name": "my-plugin",
  "description": "My development tools",
  "version": "1.0.0"
}
EOF

# 3. Add a skill
mkdir -p my-plugin/skills/hello
# Create my-plugin/skills/hello/SKILL.md

# 4. Test locally
ln -s $(pwd)/my-plugin ~/.cursor/plugins/local/my-plugin
# Reload Cursor window
```

## Marketplace

- **Official**: [cursor.com/marketplace](https://cursor.com/marketplace) — manually reviewed
- **Community**: [cursor.directory](https://cursor.directory)
- **Team marketplaces**: Private repos for Teams/Enterprise plans

## Documentation in This Collection

| Guide | Description |
|-------|-------------|
| [creating.md](creating.md) | Step-by-step plugin creation |
| [reference.md](reference.md) | Manifest schema and component formats |
| [../hooks/index.md](../hooks/index.md) | Hook configuration |
| [../skills/index.md](../skills/index.md) | Skill authoring |
| [../mcp/index.md](../mcp/index.md) | MCP server setup |
| [../rules/index.md](../rules/index.md) | Rules format |
| [../../templates/cursor-plugin.md](../../templates/cursor-plugin.md) | Starter template |

## Publishing

Submit at [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish). Plugins must be open source and pass manual review.