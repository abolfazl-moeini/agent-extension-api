# AI Coding Agent Extension Documentation

Developer-focused documentation wiki for building extensions, plugins, skills, and tools for major AI coding platforms. Designed for AI agents to generate correct, production-ready plugins.

## Start Here

| File | Purpose |
|------|---------|
| [PLUGIN-DEVELOPMENT.md](PLUGIN-DEVELOPMENT.md) | Cross-platform plugin development guide |
| [context.md](context.md) | High-level context for AI agents using this repo |
| [standards/agent-skills.md](standards/agent-skills.md) | Agent Skills open standard |
| [standards/mcp.md](standards/mcp.md) | Model Context Protocol reference |

## Platform Entry Points

Each platform has an `extension-api.md` — start there:

| Platform | Entry Point | Plugin Manifest |
|----------|-------------|-----------------|
| **Cursor** | [cursor/extension-api.md](cursor/extension-api.md) | `.cursor-plugin/plugin.json` |
| **Claude Code** | [claude-code/extension-api.md](claude-code/extension-api.md) | `.claude-plugin/plugin.json` |
| **VS Code** | [vscode/extension-api.md](vscode/extension-api.md) | `package.json` |
| **Anthropic API** | [anthropic/extension-api.md](anthropic/extension-api.md) | Skills API upload |
| **OpenAI / Codex** | [openai/extension-api.md](openai/extension-api.md) | Plugin bundle |
| **xAI / Grok** | [xai/extension-api.md](xai/extension-api.md) | Tools API + MCP |
| **MiniMax** | [minimax/extension-api.md](minimax/extension-api.md) | MCP server config |

## Documentation Map

```
agents-docs/
├── PLUGIN-DEVELOPMENT.md       # Cross-platform guide
├── context.md                  # AI agent context
├── standards/
│   ├── agent-skills.md         # SKILL.md specification
│   └── mcp.md                  # MCP configuration
├── templates/
│   ├── cursor-plugin.md        # Cursor plugin starter
│   └── claude-code-plugin.md   # Claude Code plugin starter
├── cursor/
│   ├── extension-api.md
│   ├── plugins/                # creating, reference, index
│   ├── skills/, mcp/, rules/, hooks/, agent/
├── claude-code/
│   ├── extension-api.md
│   ├── plugins/, skills/, hooks/, mcp/, agents/
├── vscode/
│   ├── extension-api/          # Getting started, guides, capabilities
│   └── language-server-protocol/
├── anthropic/
│   ├── extension-api.md
│   ├── skills-api/, api/
├── openai/
│   ├── extension-api.md
│   ├── skills/, agents-sdk/, mcp/
├── xai/
│   ├── extension-api.md
│   ├── function-calling.md, mcp.md
└── minimax/
    ├── extension-api.md
    └── mcp.md
```

## Shared Concepts (2026)

Most platforms converge on:

1. **Agent Skills** — `SKILL.md` with YAML frontmatter (open standard at [agentskills.io](https://agentskills.io))
2. **MCP** — External tool connections via Model Context Protocol
3. **Plugins** — Bundles of skills + rules + MCP + hooks for distribution
4. **Rules** — Persistent project instructions (`.mdc`, `AGENTS.md`, `CLAUDE.md`)

## Templates

Ready-to-copy plugin structures:

- [templates/cursor-plugin.md](templates/cursor-plugin.md)
- [templates/claude-code-plugin.md](templates/claude-code-plugin.md)

## Usage for AI Agents

When asked to create a plugin:

1. Read `context.md` + the target platform's `extension-api.md`
2. Check `PLUGIN-DEVELOPMENT.md` for cross-platform patterns
3. Use `standards/` for SKILL.md and MCP formats
4. Copy from `templates/` for directory structure
5. Generate complete artifacts: manifest, skills, config, testing instructions