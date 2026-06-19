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

Key files to study:
- `cursor/plugins/index.md`
- `cursor/plugins/reference.md`
- `cursor/skills/index.md`
- `cursor/mcp/index.md`

## Relevant Docs in This Collection

- `cursor/plugins/` — How to create and distribute plugins.
- `cursor/skills/` — Authoring reusable agent skills.
- `cursor/mcp/` — Connecting tools via Model Context Protocol.
- `cursor/rules/` — Persistent instructions.
- `cursor/agent/` — How the agent uses these extensions.

This is Cursor's "Extension API" equivalent.
