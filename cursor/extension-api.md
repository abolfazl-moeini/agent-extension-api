# Cursor Extension / Plugin Development (Extension API)

Cursor's extensibility system is built around **Plugins**, **Agent Skills**, **Rules**, **MCP servers**, and **Hooks**.

## Core Concepts for Plugin Developers

- **Plugins**: Installable, shareable bundles (Git repos or marketplaces). A plugin can contain any combination of:
  - Rules (`.mdc` files)
  - Skills (directories with `SKILL.md`)
  - Custom Agents
  - Commands
  - MCP Servers
  - Hooks

- **Skills**: The primary way to give the agent new capabilities. Follow the open [Agent Skills](https://agentskills.io) standard (`SKILL.md` with frontmatter).

- **MCP**: Standard way to connect external tools/data (Cursor supports stdio, SSE, Streamable HTTP).

## Creating a Plugin

1. Create a directory with `.cursor-plugin/plugin.json`:

```json
{
  "name": "my-plugin",
  "description": "...",
  "version": "1.0.0"
}
```

2. Add components in standard directories (`skills/`, `rules/`, `mcp.json`, `hooks/`, etc.).

3. Test locally:
   - Place in `~/.cursor/plugins/local/my-plugin` or use symlinks.
   - Or run with dev flags if supported.

4. Submit to Cursor Marketplace (manual review) or host your own team marketplace.

See the detailed plugin creation guide and manifest reference in the Cursor docs collection.

## Key Docs in This Collection

| Guide | Path |
|-------|------|
| Plugin creation | `cursor/plugins/creating.md` |
| Plugin reference | `cursor/plugins/reference.md` |
| Skills | `cursor/skills/index.md` |
| MCP | `cursor/mcp/index.md` |
| Rules | `cursor/rules/index.md` |
| Hooks | `cursor/hooks/index.md` |
| Agent behavior | `cursor/agent/index.md` |
| Starter template | `templates/cursor-plugin.md` |
| Shared standards | `standards/agent-skills.md`, `standards/mcp.md` |

## Testing Locally

```bash
ln -s /path/to/my-plugin ~/.cursor/plugins/local/my-plugin
# Developer: Reload Window
```

## Publishing

Submit to [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish). Plugins must be open source.
