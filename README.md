# AI Coding Agent Extension Documentation

This collection provides **developer-focused documentation** for building extensions, plugins, skills, and tools for major AI coding platforms.

## Goal

Enable AI agents to generate correct, production-ready plugins and extensions for these tools.

## Key Files

For each tool, start with its `extension-api.md`:

- `vscode/extension-api.md`
- `cursor/extension-api.md`
- `claude-code/extension-api.md`
- `anthropic/extension-api.md`
- `openai/extension-api.md`
- `xai/extension-api.md`
- `minimax/extension-api.md`

## Structure

```
<brand>/
├── extension-api.md          # How to develop extensions/plugins for this tool
└── <section>/                # Supporting detailed guides (skills, mcp, plugins, etc.)
```

## Important Context File

- `context.md` — High-level guide and context for another AI agent. Explains the extension models across tools, common patterns (Agent Skills, MCP, Plugins), how to use this repo effectively, and pitfalls to avoid.

## Brands Covered

- **VS Code** — Classic Extension API + LSP
- **Cursor** — Plugins, Agent Skills, MCP, Rules
- **Claude Code** — Plugins, Skills, Hooks, MCP, Agent SDK
- **Anthropic (Claude)** — Skills API, MCP, Agents
- **OpenAI** — Skills, Agents SDK, MCP (post-Assistants)
- **xAI (Grok)** — Function calling, Tools, MCP support
- **MiniMax** — Official MCP servers for multimodal capabilities

Use `context.md` + the relevant `*/extension-api.md` when generating plugins.
