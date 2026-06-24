# Plugin Development Guide

Complete guide for AI agents building plugins and extensions across AI coding tools.

## Quick Start by Platform

| Platform | Entry Point | Manifest Location |
|----------|-------------|-------------------|
| Cursor | `cursor/extension-api.md` | `.cursor-plugin/plugin.json` |
| Claude Code | `claude-code/extension-api.md` | `.claude-plugin/plugin.json` |
| VS Code | `vscode/extension-api.md` | `package.json` |
| OpenAI/Codex | `openai/extension-api.md` | Plugin bundle (skills + config) |
| Anthropic API | `anthropic/extension-api.md` | Skills API upload |
| xAI/Grok | `xai/extension-api.md` | Tools API + MCP |
| MiniMax | `minimax/extension-api.md` | MCP server config |

## Shared Standards

Most modern AI coding tools converge on two open standards:

1. **Agent Skills** — `SKILL.md` files with YAML frontmatter. See `standards/agent-skills.md`.
2. **MCP** — External tool connections. See `standards/mcp.md`.

## Decision Tree: What to Build

```
Need to extend an AI coding agent?
│
├─ Teach the agent a workflow or domain expertise?
│  └─ Create a SKILL.md (Agent Skills standard)
│
├─ Connect to an external API, database, or service?
│  └─ Build an MCP server
│
├─ Bundle skills + MCP + rules + automation?
│  └─ Create a plugin (Cursor or Claude Code)
│
├─ Add IDE features (syntax highlighting, debugger, UI)?
│  └─ Build a VS Code extension (possibly with LSP)
│
└─ Expose tools to Grok via API?
   └─ Function calling definitions + optional MCP server
```

## Plugin Component Matrix

| Component | Cursor | Claude Code | Codex | Purpose |
|-----------|--------|-------------|-------|---------|
| Skills | `skills/` | `skills/` | `skills/` | Agent capabilities |
| Rules | `rules/*.mdc` | `.claude/rules/` | — | Persistent instructions |
| MCP | `mcp.json` | `.mcp.json` | MCP config | External tools |
| Hooks | `hooks/` | `hooks/hooks.json` | — | Event automation |
| Agents | `agents/` | `agents/` | — | Specialized subagents |
| Commands | `commands/` | `commands/` | — | Slash commands |
| LSP | — | `.lsp.json` | — | Language intelligence |
| Monitors | — | `monitors/` | — | Background watchers |

## Minimal Plugin Examples

### Cursor Plugin

```
my-cursor-plugin/
├── .cursor-plugin/
│   └── plugin.json
├── skills/
│   └── deploy/
│       └── SKILL.md
├── rules/
│   └── coding-standards.mdc
└── mcp.json
```

`plugin.json`:
```json
{
  "name": "my-cursor-plugin",
  "description": "Deployment tools and coding standards",
  "version": "1.0.0",
  "author": { "name": "Your Name" }
}
```

Test: `~/.cursor/plugins/local/my-cursor-plugin/` then reload window.

### Claude Code Plugin

```
my-claude-plugin/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── code-reviewer/
│       └── SKILL.md
├── hooks/
│   └── hooks.json
└── .mcp.json
```

`plugin.json`:
```json
{
  "name": "my-claude-plugin",
  "description": "Code review and formatting automation",
  "version": "1.0.0"
}
```

Test: `claude --plugin-dir ./my-claude-plugin`

## SKILL.md Template

```markdown
---
name: my-skill
description: What this skill does and when to use it. Include keywords users would say.
---

# My Skill

## When to Use

- Trigger condition 1
- Trigger condition 2

## Instructions

1. Step one
2. Step two
3. Step three

## Examples

**Input**: "deploy to staging"
**Output**: Run deploy script, verify health check, report status

## Edge Cases

- If deploy fails, roll back and report error
```

## Hooks Template (Claude Code)

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "\"${CLAUDE_PLUGIN_ROOT}\"/scripts/format.sh"
          }
        ]
      }
    ]
  }
}
```

## MCP Server Template

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

## Testing Checklist

- [ ] Manifest validates (correct JSON, required fields)
- [ ] Skill `name` matches directory name
- [ ] Skill `description` includes trigger keywords
- [ ] MCP server starts and tools appear in agent
- [ ] Hooks fire on expected events
- [ ] Plugin loads locally before publishing
- [ ] No secrets committed to repository

## Publishing

| Platform | Submit To |
|----------|-----------|
| Cursor | [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish) |
| Claude Code | Plugin marketplace or private repo |
| VS Code | [marketplace.visualstudio.com](https://marketplace.visualstudio.com) |

## Common Pitfalls

| Mistake | Fix |
|---------|-----|
| Skills inside `.claude-plugin/` or `.cursor-plugin/` | Put components at plugin root, manifest in dot-directory |
| Missing `description` in SKILL.md | Agents use this for auto-discovery |
| Wrong skill namespace | Use `/plugin-name:skill-name` in Claude Code plugins |
| Deprecated OpenAI Assistants API | Migrate to Responses API + Agents SDK |
| MCP secrets in config files | Use `${env:VAR}` interpolation |
| SKILL.md over 500 lines | Split into `references/` files |

## Further Reading

- `context.md` — High-level context for AI agents using this repo
- `standards/agent-skills.md` — Full Agent Skills specification
- `standards/mcp.md` — MCP configuration and server development
- `templates/` — Starter plugin directory structures