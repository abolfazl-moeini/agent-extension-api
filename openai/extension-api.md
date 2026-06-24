# OpenAI Extension / Plugin Development (Skills, Agents SDK, MCP)

OpenAI has moved away from the deprecated Assistants API toward modern extensibility:

## Key Extension Mechanisms

### Skills (Agent Skills standard)
- `SKILL.md` files that package instructions, resources, and scripts.
- Used in Codex CLI, ChatGPT, and Agents SDK.
- Skills can be uploaded/managed and attached to environments.
- Local skills in `~/.codex/skills/` or project directories.

### Plugins (Codex)
- Bundles of skills + other components for distribution.
- Similar to Cursor/Claude Code plugin model.

### Agents SDK
- Build agentic applications with tools, handoffs, orchestration, guardrails.
- MCP support for connecting external tools.
- Sandboxed execution, evaluations, etc.

### Tools / Function Calling + MCP
- Define custom tools via function calling.
- MCP servers for standardized tool/context access.
- Skills, Shell, Computer use, File search, etc. as built-in tools.

## Developer Flow

1. Create SKILL.md following the open Agent Skills format.
2. For API usage: Upload skills or use in Responses + tools.
3. For agents: Use the Agents SDK to orchestrate with tools/MCP.
4. Package as plugins for Codex surfaces when distributing.

## Key Docs in This Collection

| Guide | Path |
|-------|------|
| Skills | `openai/skills/index.md` |
| Agents SDK | `openai/agents-sdk/index.md` |
| MCP | `openai/mcp/index.md` |
| Assistants migration | `openai/assistants/migration.md` |
| Shared standards | `standards/agent-skills.md`, `standards/mcp.md` |

**Deprecated**: Assistants API shuts down August 26, 2026. Migrate to Responses API.
