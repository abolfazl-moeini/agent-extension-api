# Claude Code Plugins Reference

Source: [code.claude.com/docs/en/plugins-reference](https://code.claude.com/docs/en/plugins-reference)

## plugin.json Schema

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Plugin identifier |
| `description` | string | What the plugin does |
| `version` | string | Semver version |
| `author` | object | `{ name, email? }` |
| `hooks` | object | Inline hook configuration |
| `mcpServers` | object | Inline MCP server config |
| `lspServers` | object | Inline LSP server config |
| `skills` | string[] | Custom skill paths |
| `agents` | string[] | Custom agent paths |
| `settings` | object | Default settings for plugin |
| `userConfig` | object | User-configurable fields |
| `dependencies` | object | Plugin dependency constraints |

## Environment Variables

| Variable | Description |
|----------|-------------|
| `${CLAUDE_PLUGIN_ROOT}` | Plugin directory path |
| `${CLAUDE_PLUGIN_DATA}` | Plugin data directory |
| `${CLAUDE_PROJECT_DIR}` | Current project directory |
| `${user_config.*}` | User configuration values |
| `${ENV_VAR}` | Shell environment variables |

## Skills

**Location**: `skills/` or `commands/` at plugin root, or `SKILL.md` at plugin root (single skill)

```
skills/
├── pdf-processor/
│   ├── SKILL.md
│   ├── reference.md
│   └── scripts/
└── code-reviewer/
    └── SKILL.md
```

If only one skill, a root `SKILL.md` works. Set frontmatter `name` explicitly — without it, marketplace installs fall back to version strings.

## Agents

**Location**: `agents/` directory

```markdown
---
name: security-auditor
description: Reviews code for security vulnerabilities. Invoke for auth, crypto, or input handling changes.
model: sonnet
effort: high
maxTurns: 20
disallowedTools: Write, Edit
---

You are a security-focused code reviewer. Analyze changes for OWASP Top 10 vulnerabilities...
```

Supported frontmatter: `name`, `description`, `model`, `effort`, `maxTurns`, `tools`, `disallowedTools`, `skills`, `memory`, `background`, `isolation` (only `"worktree"`).

Not supported in plugin agents: `hooks`, `mcpServers`, `permissionMode`.

## Hooks

**Location**: `hooks/hooks.json` or inline in `plugin.json`

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

### Hook Types

| Type | Description |
|------|-------------|
| `command` | Execute shell command |
| `http` | POST event JSON to URL |
| `mcp_tool` | Call MCP server tool |
| `prompt` | Evaluate prompt with LLM |
| `agent` | Run agentic verifier |

### Key Events

| Event | When |
|-------|------|
| `SessionStart` | Session begins or resumes |
| `UserPromptSubmit` | Before prompt processing |
| `PreToolUse` | Before tool call (can block) |
| `PostToolUse` | After successful tool call |
| `PostToolUseFailure` | After failed tool call |
| `Stop` | Claude finishes responding |
| `SessionEnd` | Session terminates |

See `../hooks/index.md` for the full event list.

## MCP Servers

**Location**: `.mcp.json` or inline in `plugin.json`

```json
{
  "mcpServers": {
    "plugin-database": {
      "command": "${CLAUDE_PLUGIN_ROOT}/servers/db-server",
      "args": ["--config", "${CLAUDE_PLUGIN_ROOT}/config.json"],
      "env": {
        "DB_PATH": "${CLAUDE_PLUGIN_ROOT}/data"
      }
    }
  }
}
```

## LSP Servers

**Location**: `.lsp.json` or inline in `plugin.json`

```json
{
  "go": {
    "command": "gopls",
    "args": ["serve"],
    "extensionToLanguage": {
      ".go": "go"
    }
  }
}
```

Language server binaries must be installed separately.

## Monitors (Experimental)

**Location**: `monitors/monitors.json` or `experimental.monitors` in `plugin.json`

```json
[
  {
    "name": "error-log",
    "command": "tail -F ./logs/error.log",
    "description": "Application error log"
  }
]
```

Requires Claude Code v2.1.105+.

## CLI Commands

```bash
claude plugin init <name>          # Scaffold plugin
claude --plugin-dir ./my-plugin    # Load for testing
claude plugin install <name>       # Install from marketplace
claude plugin list                 # List installed plugins
claude plugin uninstall <name>     # Remove plugin
```

## Related

- `index.md` — Plugin creation overview
- `../hooks/index.md` — Hook guide
- `../mcp/index.md` — MCP integration
- `../agents/index.md` — Subagent authoring