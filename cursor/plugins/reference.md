# Cursor Plugins Reference

Source: [cursor.com/docs/reference/plugins](https://cursor.com/docs/reference/plugins)

## Manifest Schema

`.cursor-plugin/plugin.json`

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Plugin identifier (lowercase, hyphens) |
| `description` | string | No | Short description for marketplace |
| `version` | string | No | Semver version |
| `author` | object | No | `{ name, email?, url? }` |
| `rules` | string[] | No | Custom paths to rule files (default: `rules/`) |
| `skills` | string[] | No | Custom paths to skill directories (default: `skills/`) |
| `agents` | string[] | No | Custom paths to agent files (default: `agents/`) |
| `commands` | string[] | No | Custom paths to command files (default: `commands/`) |
| `mcp` | string | No | Path to MCP config (default: `mcp.json`) |
| `hooks` | string | No | Path to hooks config |

## Component Formats

### Rules (`.mdc`)

```markdown
---
description: When this rule applies
globs: "**/*.ts"
alwaysApply: false
---

Rule content injected into agent context.
```

| Frontmatter | Behavior |
|-------------|----------|
| `alwaysApply: true` | Applied to every chat session |
| `description` (no globs) | Agent decides based on description |
| `globs` | Applied when matching files are in context |
| Manual | Invoked via @-mention |

### Skills (`SKILL.md`)

Follow Agent Skills standard. See `standards/agent-skills.md`.

Cursor-specific fields:

| Field | Purpose |
|-------|---------|
| `paths` | Glob patterns scoping skill to matching files |
| `disable-model-invocation` | Only loads on explicit `/skill-name` invocation |

### Agents

Markdown files in `agents/` describing custom agent configurations and prompts.

### Commands

Markdown files in `commands/` for agent-executable command definitions.

### MCP (`mcp.json`)

Standard MCP server configuration. See `standards/mcp.md`.

### Hooks

Event-driven automation scripts. The `workspaceOpen` hook can return plugin paths to load dynamically.

## Marketplace Manifest

For repos with multiple plugins, add `.cursor-plugin/marketplace.json`:

```json
{
  "name": "my-team-plugins",
  "owner": { "name": "My Team" },
  "plugins": [
    {
      "name": "plugin-a",
      "source": "./plugin-a",
      "description": "First plugin"
    },
    {
      "name": "plugin-b",
      "source": "./plugin-b",
      "description": "Second plugin"
    }
  ]
}
```

## Installation Scopes

| Scope | Location | Visibility |
|-------|----------|------------|
| User | Global settings | All projects for this user |
| Workspace | Project settings | Current project only |
| Team | Team marketplace | Distribution group members |

## Submission Checklist

- [ ] `plugin.json` with valid `name`
- [ ] Open source repository
- [ ] Skills have valid frontmatter with good descriptions
- [ ] MCP servers documented with required env vars
- [ ] No secrets in committed files
- [ ] Tested locally in `~/.cursor/plugins/local/`
- [ ] README with setup instructions

## Related

- `creating.md` — Step-by-step plugin creation
- `index.md` — Overview and marketplace info
- `../skills/index.md` — Skill authoring
- `../mcp/index.md` — MCP configuration
- `../rules/index.md` — Rules format