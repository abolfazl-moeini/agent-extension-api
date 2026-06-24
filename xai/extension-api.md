# xAI / Grok Extension Development (Tools, Function Calling, MCP)

xAI focuses on a powerful API with built-in tool use rather than a traditional plugin marketplace.

## Primary Extension Points

### Function Calling / Tools
- Define custom tools that Grok can call (similar to OpenAI function calling).
- The model decides when to invoke your tools and provides structured arguments.
- Supports web search, image generation, vision, etc. as first-class tools.

### MCP Support
- Grok Build and API support Model Context Protocol.
- You can connect external MCP servers or build your own to expose tools to Grok agents.
- Community and official MCP servers exist for Grok (image, chat, search, video).

### Agentic Coding (Grok Build)
- Grok Build CLI is an agentic coding tool with MCP compatibility.
- Designed for multi-step workflows, planning, and tool use.

## How to "Extend" Grok

1. **Custom Tools**: Implement tools in your application and expose them via the Responses / chat completions API with tool definitions.
2. **MCP Servers**: Build or run an MCP server (stdio/SSE/HTTP) that Grok agents can connect to for new capabilities.
3. **Integrate into coding agents**: Use xAI models inside Cursor, Claude Code, or your own agent frameworks via compatible APIs or MCP.

## Key Docs in This Collection

| Guide | Path |
|-------|------|
| API overview | `xai/overview.md` |
| Function calling | `xai/function-calling.md` |
| MCP integration | `xai/mcp.md` |
| Shared standards | `standards/mcp.md` |

Grok Build CLI supports MCP for agentic coding workflows.
