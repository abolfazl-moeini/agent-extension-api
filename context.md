This repository is a curated developer wiki for building extensions, plugins, skills, and tools for major AI coding agents and platforms.

## Purpose

Enable an AI coding agent to:
- Understand the extension/plugin architecture of each tool
- Generate correct code, manifests, SKILL.md files, MCP servers, hooks, etc.
- Follow current (2026) best practices and standards

## Repository Structure

```
<brand>/
  extension-api.md          ← START HERE for each tool
  <section>/
    index.md or specific guides

standards/                  ← Shared open standards
templates/                  ← Starter plugin structures
PLUGIN-DEVELOPMENT.md       ← Cross-platform guide
```

**Brands**: `vscode/`, `cursor/`, `claude-code/`, `anthropic/`, `openai/`, `xai/`, `minimax/`

## Current State of AI Coding Tool Extensibility (2026)

### 1. Agent Skills (open standard)
- Defined in `SKILL.md` with YAML frontmatter (`name`, `description`, instructions)
- Supports dynamic injection (`!command` in Claude Code)
- User-invoked (`/skill-name`) or auto-discovered by the agent
- Used by: Cursor, Claude Code, Codex/OpenAI, and others
- Full spec: `standards/agent-skills.md`

### 2. MCP (Model Context Protocol)
- Standard for connecting agents to external tools and data
- Transports: stdio, SSE, Streamable HTTP
- Supported by Cursor, Claude Code, OpenAI Agents SDK, xAI Grok Build, MiniMax
- Full reference: `standards/mcp.md`

### 3. Plugins / Bundles
- Distribution unit packaging Skills + Rules + Agents + MCP + Hooks
- Manifest: `plugin.json` in `.cursor-plugin/` or `.claude-plugin/`
- Marketplaces: Cursor, Claude Code, Codex
- Templates: `templates/cursor-plugin.md`, `templates/claude-code-plugin.md`

### 4. Rules / Persistent Instructions
- Project-level: `.cursor/rules/*.mdc`, `AGENTS.md`, `CLAUDE.md`
- Applied automatically, by glob, or via @-mention

## Workflow for AI Agents

When asked to create a plugin/extension:

1. Read the brand's `extension-api.md`
2. Read `PLUGIN-DEVELOPMENT.md` for cross-platform patterns
3. Dive into relevant sections (skills, MCP, plugins, hooks, rules)
4. Use `templates/` for directory structure
5. Follow exact namespacing and file placement rules
6. Generate complete, ready-to-test artifacts

## Tool-Specific Notes

**VS Code** — Traditional extension API. `package.json` contribution points + activation events. Prefer LSP for language features. No DOM access in extension host.

**Cursor** — Modern plugin system: Skills + MCP + Rules. Manifest at `.cursor-plugin/plugin.json`. Test in `~/.cursor/plugins/local/`. Submit to Cursor Marketplace.

**Claude Code** — Richest plugin model: skills, agents, hooks, MCP, LSP, monitors. Manifest at `.claude-plugin/plugin.json`. Test with `claude --plugin-dir`. Skills namespaced as `/plugin-name:skill-name`.

**Anthropic / Claude API** — Skills API for programmatic upload. MCP connector in Messages API. Plugins are primarily a Claude Code concept.

**OpenAI / Codex** — Skills + Agents SDK + MCP. Assistants API deprecated (Aug 2026). Use Responses API. Skills in `~/.codex/skills/`.

**xAI / Grok** — Function calling + MCP. Grok Build CLI for agentic coding. OpenAI-compatible API at `api.x.ai/v1`.

**MiniMax** — Official MCP servers for multimodal (voice, image, video, music). Drop into any MCP client.

## Common Pitfalls

| Mistake | Fix |
|---------|-----|
| Components inside `.claude-plugin/` or `.cursor-plugin/` | Put at plugin root; only manifest in dot-directory |
| Missing `description` in SKILL.md | Agents rely on this for auto-discovery |
| Wrong skill namespace | Claude Code: `/plugin-name:skill-name` |
| Deprecated OpenAI Assistants API | Use Responses API + Agents SDK |
| Secrets in config files | Use `${env:VAR}` interpolation |
| SKILL.md over 500 lines | Split into `references/` files |

## Recommended Output When Creating a Plugin

Provide:
- Complete directory tree
- All manifest files (`plugin.json`, `.mcp.json`, `hooks.json`)
- At least one well-written `SKILL.md` with good description
- Configuration snippets for the target client
- Testing instructions (`--plugin-dir`, reload commands, etc.)

Use this repo as ground truth for formats and best practices.