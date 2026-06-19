# Anthropic / Claude Extension Development (Skills, Agents, MCP)

Anthropic provides several mechanisms to extend Claude:

## Primary Extension Mechanisms

### Agent Skills (Core "Extension" Format)
- Skills are bundles with a `SKILL.md` (frontmatter + instructions + optional scripts/references).
- Can be used in:
  - Claude Code (local files or plugins)
  - Claude API (upload via Skills API)
  - claude.ai

- Create custom skills and upload via `/v1/skills` endpoints.
- Pre-built skills (e.g., pptx, xlsx) available by ID.

### MCP (Model Context Protocol)
- Connect external tools and data sources.
- MCP Connector in Messages API.
- Build MCP servers for custom capabilities.

### Agents API + Sessions
- Define reusable, versioned agent configurations.
- Stateful sessions in managed sandboxes.

### Custom Tools
- Function calling / tool use in the Messages API.

## Developer Flow for "Plugins/Extensions"

1. Author a Skill (SKILL.md following the open standard).
2. For sharing: Package as a Claude Code plugin or upload via Skills API.
3. For tools/context: Implement or connect an MCP server.
4. Use in API calls or in Claude Code / Desktop.

Key resources in this collection:
- `anthropic/api/getting-started.md`
- `claude-code/skills/skills.md` (very detailed)
- `claude-code/extension-api.md` (cross reference)

See the Skills API reference and Agent Skills guides for full schemas and best practices.

This is Anthropic's extension model.
