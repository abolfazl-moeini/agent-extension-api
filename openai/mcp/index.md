# OpenAI MCP Integration

Source: [developers.openai.com](https://developers.openai.com)

OpenAI supports Model Context Protocol in the Agents SDK and Responses API.

## Agents SDK MCP

```python
from agents.mcp import MCPServerStdio

server = MCPServerStdio(
    name="my-tools",
    params={
        "command": "python",
        "args": ["-m", "my_mcp_server"],
        "env": {"API_KEY": os.environ["API_KEY"]},
    },
)

agent = Agent(name="Tool Agent", mcp_servers=[server])
```

## Responses API Tools

Include MCP tools in API requests alongside function calling:

- MCP servers expose tools the model can invoke
- Tools return structured results to the conversation
- Combine with built-in tools (web search, file search, etc.)

## Building MCP Servers

See `standards/mcp.md` for server development patterns.

Common server types for coding agents:
- Database query servers
- API integration servers
- Documentation search servers
- CI/CD trigger servers

## Connectors

OpenAI provides managed connectors for common services. Custom MCP servers extend this for proprietary tools.

## Related

- `../../standards/mcp.md` — Cross-platform MCP reference
- `../agents-sdk/index.md` — Agents SDK guide
- `../skills/index.md` — Skills integration