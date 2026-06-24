# Claude Code Subagents

Source: [code.claude.com/docs/en/sub-agents](https://code.claude.com/docs/en/sub-agents)

Subagents are specialized AI assistants for focused tasks. Package them in plugins via the `agents/` directory.

## Agent File Format

```markdown
---
name: code-reviewer
description: Reviews code for bugs, security issues, and style. Invoke when reviewing PRs or after significant changes.
model: sonnet
effort: medium
maxTurns: 15
disallowedTools: Write, Edit
---

You are a senior code reviewer. Focus on:
- Logic errors and edge cases
- Security vulnerabilities (OWASP Top 10)
- Test coverage gaps
- Code clarity and maintainability

Provide feedback grouped by severity: critical, warning, suggestion.
```

## Frontmatter Fields

| Field | Description |
|-------|-------------|
| `name` | Agent identifier |
| `description` | When Claude should invoke this agent |
| `model` | Model alias (`sonnet`, `opus`, `haiku`) |
| `effort` | Reasoning effort (`low`, `medium`, `high`) |
| `maxTurns` | Maximum agent turns |
| `tools` | Allowed tools (whitelist) |
| `disallowedTools` | Blocked tools |
| `skills` | Skills available to this agent |
| `memory` | Persistent memory configuration |
| `background` | Run in background |
| `isolation` | Only `"worktree"` — run in git worktree |

## Plugin Location

```
my-plugin/
└── agents/
    ├── code-reviewer.md
    ├── security-auditor.md
    └── test-writer.md
```

## Invocation

- **Automatic**: Claude invokes based on task context and `description`
- **Manual**: User invokes via `/agents` interface
- **From skills**: Set `context: fork` + `agent: <name>` in SKILL.md

## Skill-Based Subagents

In `SKILL.md`:

```markdown
---
name: deep-analysis
description: Perform deep codebase analysis
context: fork
agent: Explore
---
```

Runs the skill in an isolated subagent context.

## Restrictions in Plugin Agents

Not supported for plugin-shipped agents:
- `hooks`
- `mcpServers`
- `permissionMode`

## Related

- `../plugins/reference.md` — Agent schema in plugins
- `../skills/skills.md` — Skill-based forking
- [Agent teams](https://code.claude.com/docs/en/agent-teams) — Multi-agent orchestration