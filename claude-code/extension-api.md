# Claude Code Plugin & Extension Development (Extension API)

Claude Code has a rich plugin and extension system centered on **Plugins**, **Skills**, **MCP**, **Hooks**, **Agents**, and the **Agent SDK**.

## Plugin System

Plugins are self-contained directories with a manifest:

```json
{
  "name": "my-plugin",
  "description": "...",
  "version": "1.0.0"
}
```

Location of components (at plugin root, **not** inside `.claude-plugin/`):
- `skills/<name>/SKILL.md`
- `agents/`
- `hooks/hooks.json`
- `.mcp.json`
- `settings.json`
- `bin/`
- etc.

## Key Development Workflows

- Use `claude --plugin-dir ./my-plugin` for local testing.
- `claude plugin init` for scaffolding.
- Skills use the open Agent Skills standard.
- Namespacing: Plugin skills appear as `/my-plugin:skill-name`.
- Convert standalone `.claude/` configs to plugins for sharing.

## Other Extension Points

- **Skills API** (for Claude API users): Upload and manage custom skills programmatically.
- **MCP**: Build or connect MCP servers for tools and context.
- **Agent SDK**: Build custom agents programmatically (Python/TypeScript).
- **Hooks**: Automate behavior on tool events.

## How to Develop

1. Start with a skill in `SKILL.md` (frontmatter + instructions, dynamic injection with `!cmd`).
2. Package into a plugin with manifest.
3. Add MCP, hooks, agents as needed.
4. Distribute via marketplace or private repo.

Full details in:
- `claude-code/skills/skills.md`
- Official plugins and plugins-reference docs (see llms.txt for index).

This is the equivalent of an "Extension API" for Claude Code.
