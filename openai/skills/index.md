# OpenAI / Codex Skills

Source: [developers.openai.com](https://developers.openai.com)

Skills package domain expertise using the open Agent Skills standard (`SKILL.md`).

## Skill Locations

| Location | Scope |
|----------|-------|
| `~/.codex/skills/<name>/SKILL.md` | User-level |
| `.codex/skills/<name>/SKILL.md` | Project-level |
| Plugin `skills/` directory | Bundled in Codex plugins |

Cursor also loads `.codex/skills/` for compatibility.

## SKILL.md Format

```markdown
---
name: api-design
description: Design REST API endpoints with proper schemas, error handling, and versioning. Use when creating or reviewing API routes.
---

# API Design

## Instructions

1. Define resource models with clear naming
2. Use standard HTTP methods and status codes
3. Include pagination, filtering, and error schemas
4. Document with OpenAPI
```

See `standards/agent-skills.md` for the full specification.

## Skills in the API

Upload and manage skills programmatically:

- Attach skills to agent environments
- Skills provide instructions and resources the model can use
- Combine with function calling and MCP tools

## Codex Plugins

Bundle skills with other components for distribution:

```
my-codex-plugin/
├── skills/
│   └── deploy/
│       └── SKILL.md
└── plugin.json
```

Similar to Cursor and Claude Code plugin models.

## Migration Note

The Assistants API is deprecated (shutdown August 26, 2026). Use:
- **Responses API** for conversations
- **Agents SDK** for orchestration
- **Skills** for domain expertise
- **MCP** for external tools

See `../assistants/migration.md`.

## Related

- `../extension-api.md` — OpenAI extension overview
- `../agents-sdk/index.md` — Agents SDK guide
- `../mcp/index.md` — MCP integration