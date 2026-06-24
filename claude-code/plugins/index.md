# Claude Code Plugins

Source: [code.claude.com/docs/en/plugins](https://code.claude.com/docs/en/plugins)

## Overview

Plugins are self-contained directories that extend Claude Code with skills, agents, hooks, MCP servers, LSP servers, and monitors.

## Quick Start

```bash
# Scaffold a new plugin
claude plugin init my-plugin

# Test locally
claude --plugin-dir ./my-plugin
```

## Directory Structure

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── code-reviewer/
│       └── SKILL.md
├── agents/
│   └── security-auditor.md
├── hooks/
│   └── hooks.json
├── .mcp.json
├── .lsp.json
├── monitors/
│   └── monitors.json
├── bin/
│   └── helper-script
└── settings.json
```

**Important**: Components live at the plugin root, not inside `.claude-plugin/`.

## Manifest

```json
{
  "name": "my-plugin",
  "description": "Code review and security tools",
  "version": "1.0.0",
  "author": {
    "name": "Your Name"
  }
}
```

## Skill Namespacing

Plugin skills are invoked as `/plugin-name:skill-name`. For example, a skill `code-reviewer` in plugin `my-plugin` is `/my-plugin:code-reviewer`.

## Installation Scopes

| Scope | Settings File | Use Case |
|-------|---------------|----------|
| `user` | `~/.claude/settings.json` | Personal, all projects |
| `project` | `.claude/settings.json` | Team-shared via git |
| `local` | `.claude/settings.local.json` | Project-specific, gitignored |
| `managed` | Managed settings | Organization-wide, read-only |

## Skills-Directory Plugins

Folders under skills directories with `.claude-plugin/plugin.json` auto-load as plugins:

| Location | Scope |
|----------|-------|
| `~/.claude/skills/<name>/.claude-plugin/` | Personal, all projects |
| `<project>/.claude/skills/<name>/.claude-plugin/` | Project (requires trust) |

## Distribution

- **Marketplace**: Submit to Claude Code plugin marketplaces
- **Private repo**: Host a marketplace manifest for team distribution
- **Local**: `claude --plugin-dir` for development

See `reference.md` for complete schemas and CLI commands.

## Related

- `../skills/skills.md` — Skill authoring
- `../hooks/index.md` — Hook events and configuration
- `../mcp/index.md` — MCP server bundling
- `../agents/index.md` — Subagent definitions