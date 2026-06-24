# Anthropic Skills API

Source: [platform.claude.com/docs](https://platform.claude.com/docs)

Upload and manage custom skills programmatically via the Claude API.

## Overview

Skills are bundles with a `SKILL.md` (frontmatter + instructions + optional scripts/references). The Skills API lets you:

- Create custom skills
- Upload skill files
- Attach skills to API requests
- Use pre-built Anthropic skills (pptx, xlsx, docx, etc.)

## API Endpoints (Beta)

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/v1/skills` | POST | Create a skill |
| `/v1/skills/{id}` | GET | Retrieve skill |
| `/v1/skills/{id}` | DELETE | Delete skill |
| `/v1/skills` | GET | List skills |

## Authentication

```bash
curl https://api.anthropic.com/v1/skills \
  -H "x-api-key: $ANTHROPIC_API_KEY" \
  -H "anthropic-version: 2023-06-01" \
  -H "content-type: application/json"
```

## Using Skills in Messages

Attach skills to Messages API requests:

```python
import anthropic

client = anthropic.Anthropic()

response = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=4096,
    messages=[{"role": "user", "content": "Create a quarterly report spreadsheet"}],
    tools=[{
        "type": "skill",
        "skill_id": "xlsx",
    }],
)
```

## Pre-built Skills

Anthropic provides bundled skills by ID:

| ID | Purpose |
|----|---------|
| `pptx` | PowerPoint creation and editing |
| `xlsx` | Spreadsheet operations |
| `docx` | Word document manipulation |
| `pdf` | PDF processing |

## Custom Skill Format

Follow the Agent Skills standard:

```
my-skill/
├── SKILL.md
├── scripts/
│   └── process.py
└── references/
    └── SCHEMA.md
```

```markdown
---
name: quarterly-report
description: Generate quarterly business reports with charts and summaries. Use when creating financial or operational reports.
---

# Quarterly Report Generator

## Instructions
1. Gather metrics from provided data sources
2. Generate summary tables
3. Create visualizations
4. Format as presentation or document
```

## MCP Connector

Combine skills with MCP for external tool access in the Messages API:

```python
response = client.messages.create(
    model="claude-sonnet-4-20250514",
    messages=[...],
    mcp_servers=[{
        "type": "url",
        "url": "https://mcp.example.com/sse",
        "name": "my-tools",
    }],
)
```

## Claude Code vs API Skills

| Context | How Skills Work |
|---------|-----------------|
| Claude Code | Local files, plugins, `~/.claude/skills/` |
| Claude API | Upload via Skills API, attach by ID |
| claude.ai | User-uploaded skills |

Package Claude Code plugins for local use; use Skills API for programmatic API access.

## Related

- `../../standards/agent-skills.md` — Skill format specification
- `../../claude-code/skills/skills.md` — Claude Code skill authoring
- `../extension-api.md` — Anthropic extension overview
- `../api/getting-started.md` — API authentication and setup