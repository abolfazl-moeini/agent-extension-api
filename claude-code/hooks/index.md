# Claude Code Hooks

Source: [code.claude.com/docs/en/hooks](https://code.claude.com/docs/en/hooks)

Hooks automate actions in response to Claude Code lifecycle events. Package them in plugins via `hooks/hooks.json`.

## Configuration

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "prettier --write \"$CLAUDE_FILE_PATH\""
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Claude finished\"'"
          }
        ]
      }
    ]
  }
}
```

## Hook Types

| Type | Description |
|------|-------------|
| `command` | Run shell command or script |
| `http` | POST event JSON to a URL |
| `mcp_tool` | Invoke an MCP server tool |
| `prompt` | Evaluate a prompt with an LLM (`$ARGUMENTS` for context) |
| `agent` | Run an agentic verifier with tools |

## Common Events

| Event | When | Can Block? |
|-------|------|------------|
| `SessionStart` | Session begins or resumes | No |
| `UserPromptSubmit` | User submits a prompt | Yes |
| `PreToolUse` | Before tool executes | Yes |
| `PermissionRequest` | Permission dialog shown | Yes |
| `PostToolUse` | After successful tool call | No |
| `PostToolUseFailure` | After failed tool call | No |
| `Stop` | Claude finishes responding | No |
| `SessionEnd` | Session terminates | No |
| `PreCompact` | Before context compaction | No |
| `PostCompact` | After compaction completes | No |
| `FileChanged` | Watched file changes on disk | No |
| `WorktreeCreate` | Worktree being created | Yes |
| `WorktreeRemove` | Worktree being removed | No |

## Matchers

The `matcher` field filters which tools trigger the hook:

```json
{
  "matcher": "Write|Edit|Bash",
  "hooks": [...]
}
```

Omit `matcher` to match all events of that type.

## Plugin Hooks

In plugins, use `${CLAUDE_PLUGIN_ROOT}` for script paths:

```json
{
  "type": "command",
  "command": "\"${CLAUDE_PLUGIN_ROOT}\"/scripts/lint.sh"
}
```

## Use Cases

- Auto-format code after edits
- Run linters on changed files
- Send notifications when tasks complete
- Block dangerous commands in `PreToolUse`
- Inject context before prompt processing
- Validate output with agentic verifiers

## Debugging

```bash
# Inside Claude Code session
/hooks    # View loaded hooks
/doctor   # Diagnose configuration issues
```

## Related

- `../plugins/reference.md` — Plugin hook schema
- [Hooks guide](https://code.claude.com/docs/en/hooks-guide) — Step-by-step tutorials