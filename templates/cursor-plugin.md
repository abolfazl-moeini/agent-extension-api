# Cursor Plugin Template

Copy this structure to start a new Cursor plugin.

## Directory Tree

```
my-cursor-plugin/
├── .cursor-plugin/
│   └── plugin.json
├── README.md
├── rules/
│   └── project-standards.mdc
├── skills/
│   └── code-reviewer/
│       ├── SKILL.md
│       └── references/
│           └── CHECKLIST.md
├── agents/
│   └── security-reviewer.md
├── commands/
│   └── run-tests.md
└── mcp.json
```

## plugin.json

```json
{
  "name": "my-cursor-plugin",
  "description": "Code review, security checks, and project standards",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "email": "you@example.com"
  }
}
```

## rules/project-standards.mdc

```markdown
---
description: Project coding standards and conventions
alwaysApply: true
---

- Use TypeScript strict mode
- Write tests for all new functions
- Follow existing naming conventions in the codebase
```

## skills/code-reviewer/SKILL.md

```markdown
---
name: code-reviewer
description: Review code for bugs, security issues, and style violations. Use when reviewing PRs, diffs, or when the user asks for a code review.
paths: "**/*.{ts,tsx,js,jsx}"
---

# Code Reviewer

## Process

1. Read the changed files
2. Check for logic errors, security issues, missing tests
3. Verify naming and style match project conventions
4. Report findings grouped by severity

See [checklist](references/CHECKLIST.md) for detailed criteria.
```

## agents/security-reviewer.md

```markdown
---
name: security-reviewer
description: Security-focused code review for auth, crypto, and input handling
---

Review code changes for security vulnerabilities. Focus on injection, auth bypass, and data exposure.
```

## mcp.json

```json
{
  "mcpServers": {
    "project-docs": {
      "command": "npx",
      "args": ["-y", "my-docs-mcp-server"],
      "env": {
        "DOCS_PATH": "${workspaceFolder}/docs"
      }
    }
  }
}
```

## Local Testing

```bash
ln -s $(pwd) ~/.cursor/plugins/local/my-cursor-plugin
# Reload Cursor window
```