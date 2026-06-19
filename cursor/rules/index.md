# Rules | Cursor Docs

Source: https://cursor.com/docs/rules

# Rules

Rules provide system-level instructions to Agent. They bundle prompts, scripts, and more together, making it easy to manage and share workflows across your team.

Cursor supports four types of rules:

### Project Rules

Stored in `.cursor/rules`, version-controlled and scoped to your codebase.

### User Rules

Global to your Cursor environment. Used by Agent (Chat).

### Team Rules

Team-wide rules managed from the dashboard. Available on Team and Enterprise plans.

### AGENTS.md

Agent instructions in markdown format. Simple alternative to `.cursor/rules`.

## How rules work

Large language models don't retain memory between completions. Rules provide persistent, reusable context at the prompt level.

When applied, rule contents are included at the start of the model context.

## Project rules

Project rules live in `.cursor/rules` as `.mdc` files and are version-controlled.

### Rule file structure

Each rule is an `.mdc` file.

```bash
.cursor/rules/
  react-patterns.mdc
  frontend/
    components.mdc
```

### Rule anatomy

Frontmatter controls application:

- `alwaysApply: true` — Apply to every chat session
- `description` + no globs — Agent decides based on description ("Apply Intelligently")
- `globs` — Apply to specific files
- Manual via @-mention

See the full frontmatter table and examples in the source page.

## Best practices

- Keep rules under 500 lines
- Split large rules
- Provide concrete examples
- Reference files with `@filename`
- Check rules into git

## Team Rules

Admins manage from Cursor dashboard. Can be enforced.

Precedence: Team Rules → Project Rules → User Rules.

## AGENTS.md

Simple markdown file for agent instructions placed in project root or subdirs. Nested AGENTS.md supported.

## User Rules

Global preferences in Cursor Settings → Rules.

## FAQ

See source for troubleshooting and more.

---

## Sitemap

[Overview of all docs pages](/llms.txt)
