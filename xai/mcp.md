# xAI MCP Integration

Source: [docs.x.ai](https://docs.x.ai)

Grok Build and the xAI API support Model Context Protocol for connecting external tools.

## Grok Build MCP

Configure MCP servers in Grok Build settings or project config:

```json
{
  "mcpServers": {
    "my-tools": {
      "command": "npx",
      "args": ["-y", "my-mcp-server"],
      "env": {
        "API_KEY": "${env:MY_API_KEY}"
      }
    }
  }
}
```

Grok Build discovers MCP tools and makes them available to the agent during coding sessions.

## Building MCP Servers for Grok

Follow standard MCP patterns. See `standards/mcp.md`.

```python
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("grok-tools")

@mcp.tool()
def search_codebase(query: str) -> str:
    """Search the project codebase for matching code."""
    # Implementation
    return results

if __name__ == "__main__":
    mcp.run()
```

## Community MCP Servers

Community servers exist for Grok-specific capabilities:
- Image generation
- Web search
- Video processing
- Chat integrations

## Integration with Other Agents

Use xAI models inside other coding agents:

| Method | Description |
|--------|-------------|
| OpenAI-compatible API | `base_url: https://api.x.ai/v1` |
| MCP server | Expose xAI tools to any MCP client |
| Function calling | Define tools in your application |

## Related

- `function-calling.md` — Custom tool definitions
- `overview.md` — API quickstart
- `../../standards/mcp.md` — MCP reference