# Claude Code Plugin Template

Copy this structure to start a new Claude Code plugin.

## Directory Tree

```
my-claude-plugin/
├── .claude-plugin/
│   └── plugin.json
├── README.md
├── skills/
│   ├── code-reviewer/
│   │   ├── SKILL.md
│   │   └── scripts/
│   │       └── lint.sh
│   └── deploy/
│       └── SKILL.md
├── agents/
│   └── security-auditor.md
├── hooks/
│   └── hooks.json
├── .mcp.json
└── bin/
    └── format-all.sh
```

## plugin.json

```json
{
  "name": "my-claude-plugin",
  "description": "Code review, deployment, and formatting automation",
  "version": "1.0.0",
  "author": {
    "name": "Your Name"
  }
}
```

## skills/code-reviewer/SKILL.md

```markdown
---
name: code-reviewer
description: Review code for bugs, security, and style. Use when reviewing PRs or after significant changes.
allowed-tools: Read Grep
---

# Code Reviewer

## Process

1. Read changed files
2. Check logic, security, test coverage
3. Report by severity: critical, warning, suggestion

Current diff:
!`git diff HEAD`
```

## skills/deploy/SKILL.md

```markdown
---
name: deploy
description: Deploy application to staging or production. Use when the user asks to deploy, ship, or release.
disable-model-invocation: true
---

# Deploy

## Staging

1. Run tests: `npm test`
2. Build: `npm run build`
3. Deploy: `npm run deploy:staging`
4. Verify health check endpoint
```

## agents/security-auditor.md

```markdown
---
name: security-auditor
description: Security review for auth, crypto, input validation, and secrets handling
model: sonnet
effort: high
maxTurns: 20
disallowedTools: Write, Edit
---

You are a security auditor. Check for OWASP Top 10, secret exposure, and insecure defaults.
```

## hooks/hooks.json

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "\"${CLAUDE_PLUGIN_ROOT}\"/bin/format-all.sh"
          }
        ]
      }
    ]
  }
}
```

## .mcp.json

```json
{
  "mcpServers": {
    "ci-status": {
      "command": "npx",
      "args": ["-y", "my-ci-mcp-server"],
      "env": {
        "CI_TOKEN": "${env:CI_TOKEN}"
      }
    }
  }
}
```

## Local Testing

```bash
claude plugin init my-claude-plugin   # Or copy this template
claude --plugin-dir ./my-claude-plugin

# Invoke namespaced skills
# /my-claude-plugin:code-reviewer
# /my-claude-plugin:deploy
```