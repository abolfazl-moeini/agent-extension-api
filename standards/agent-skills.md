# Agent Skills Standard

Source: [agentskills.io](https://agentskills.io/specification)

Agent Skills is the open standard for extending AI coding agents. Cursor, Claude Code, Codex/OpenAI, and other tools share this format.

## Directory Structure

```
skill-name/
├── SKILL.md          # Required: metadata + instructions
├── scripts/          # Optional: executable code
├── references/       # Optional: documentation
└── assets/           # Optional: templates, resources
```

The `name` in frontmatter must match the parent directory name.

## SKILL.md Format

```markdown
---
name: code-review
description: Review code for bugs, security issues, and style. Use when reviewing PRs, diffs, or when the user asks for a code review.
---

# Code Review

## Instructions

1. Read the changed files
2. Check for logic errors, security issues, and test coverage
3. Provide actionable feedback grouped by severity
```

## Frontmatter Fields

| Field | Required | Constraints |
|-------|----------|-------------|
| `name` | Yes | 1–64 chars, lowercase alphanumeric + hyphens, no leading/trailing hyphens |
| `description` | Yes | 1–1024 chars; describe what it does and when to use it |
| `license` | No | License name or reference to bundled license file |
| `compatibility` | No | Max 500 chars; environment requirements |
| `metadata` | No | Arbitrary key-value map |
| `allowed-tools` | No | Space-separated pre-approved tools (experimental) |

### Platform-Specific Extensions

Some platforms add fields beyond the open standard:

| Field | Platform | Purpose |
|-------|----------|---------|
| `paths` | Cursor | Glob patterns to scope skill to matching files |
| `disable-model-invocation` | Cursor, Claude Code | Skill only loads when user invokes `/skill-name` |
| `context: fork` | Claude Code | Run skill in isolated subagent context |
| `agent` | Claude Code | Subagent type when `context: fork` is set |
| `hooks` | Claude Code | Inline hook configuration for skill lifecycle |

## Skill Discovery Locations

| Location | Scope | Tools |
|----------|-------|-------|
| `.agents/skills/` | Project | Cursor (preferred) |
| `.cursor/skills/` | Project | Cursor |
| `.claude/skills/` | Project | Claude Code, Cursor (compat) |
| `.codex/skills/` | Project | Codex/OpenAI, Cursor (compat) |
| `~/.agents/skills/` | User | Cursor |
| `~/.cursor/skills/` | User | Cursor |
| `~/.claude/skills/` | User | Claude Code |
| `~/.codex/skills/` | User | Codex/OpenAI |
| `skills/<name>/SKILL.md` | Plugin | Cursor, Claude Code plugins |

## Dynamic Context Injection (Claude Code)

Inject live data before the skill reaches the model:

```markdown
Current diff:
!`git diff HEAD`
```

Or fenced blocks:

````
```!
git log --oneline -5
```
````

## Progressive Disclosure

Agents load skills in layers:

1. **Metadata** (~100 tokens): `name` + `description` at startup for all skills
2. **Instructions** (<5000 tokens recommended): full `SKILL.md` body when activated
3. **Resources** (on demand): `scripts/`, `references/`, `assets/` files

Keep `SKILL.md` under 500 lines. Move detailed reference material to `references/`.

## Validation

```bash
# Using the official reference library
skills-ref validate ./my-skill
```

## Best Practices for AI-Generated Skills

- Write `description` in natural language the user would actually say
- Include trigger keywords: file types, task names, tool names
- Provide step-by-step instructions, not vague guidance
- Include concrete examples of inputs and expected outputs
- Reference supporting files with relative paths one level deep
- Test invocation via `/skill-name` and auto-discovery

## Plugin Namespacing

When packaged in a plugin, skills are namespaced:

| Platform | Invocation |
|----------|------------|
| Claude Code | `/plugin-name:skill-name` |
| Cursor | `/skill-name` (plugin skills appear in skill list) |
| Codex | `/skill-name` |