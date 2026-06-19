# Extend Claude with Skills (Comprehensive)

Source: https://code.claude.com/docs/en/skills + related

Claude Code uses the Agent Skills open standard.

## Creating a Skill

1. Create directory: `~/.claude/skills/my-skill/` or `.claude/skills/my-skill/`
2. Add `SKILL.md` with YAML frontmatter + instructions.

Example frontmatter fields:
- name, description
- disable-model-invocation
- allowed-tools
- context: fork (for subagents)
- paths (globs for scoping)
- hooks
- arguments for $ARGUMENTS substitution

## Dynamic Context Injection

Use `!`command`` syntax or fenced ```! blocks. Commands run before the skill content reaches the model.

Example:
```
Current diff:
!`git diff HEAD`
```

## Subagents & Forking

Set `context: fork` + `agent: Explore|Plan|...` to run the skill in an isolated agent context.

## Supporting Files

skills/my-skill/
├── SKILL.md
├── scripts/
├── references/
└── assets/

Reference them from SKILL.md so they load on demand.

## Bundled Skills, Plugins, and Distribution

- Bundled skills ship with Claude Code
- Package skills inside plugins (with .cursor-plugin or equivalent manifest)
- Enterprise managed skills via settings

## Best Practices & Evals

- Keep SKILL.md focused (<500 lines)
- Use skill-creator plugin for evals, benchmarks, A/B testing
- Prefer `description` that matches natural user language

## Related

- Hooks
- Sub-agents
- MCP
- Permissions
- CLAUDE.md (for persistent project instructions)

See the full official documentation and llms.txt for the complete reference.
