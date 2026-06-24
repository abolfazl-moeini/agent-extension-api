# Model Context Protocol (MCP)

Source: [modelcontextprotocol.io](https://modelcontextprotocol.io)

MCP is the open standard for connecting AI agents to external tools, data sources, and services. It is supported by Cursor, Claude Code, OpenAI Agents SDK, xAI Grok Build, MiniMax, and many other clients.

## Core Concepts

| Concept | Description |
|---------|-------------|
| **MCP Server** | Exposes tools, prompts, and resources to agents |
| **MCP Client** | The agent host (Cursor, Claude Code, etc.) that connects to servers |
| **Transport** | How client and server communicate |
| **Tool** | Callable function the agent can invoke |
| **Resource** | Readable data (files, records, etc.) |
| **Prompt** | Pre-built prompt templates |

## Transport Types

| Transport | Use Case | Config |
|-----------|----------|--------|
| **stdio** | Local processes | `command` + `args` |
| **SSE** | Local or remote HTTP | `url` with SSE endpoint |
| **Streamable HTTP** | Local or remote HTTP | `url` with HTTP transport |

## Configuration Formats

### Cursor (`mcp.json`)

Project: `.cursor/mcp.json`  
Global: `~/.cursor/mcp.json`

```json
{
  "mcpServers": {
    "my-server": {
      "command": "npx",
      "args": ["-y", "my-mcp-server"],
      "env": {
        "API_KEY": "${env:MY_API_KEY}"
      }
    },
    "remote-server": {
      "url": "https://mcp.example.com/sse"
    }
  }
}
```

### Claude Code (`.mcp.json`)

Project: `.mcp.json` in project root  
Plugin: `.mcp.json` in plugin root

```json
{
  "mcpServers": {
    "database": {
      "command": "${CLAUDE_PLUGIN_ROOT}/servers/db-server",
      "args": ["--config", "${CLAUDE_PLUGIN_ROOT}/config.json"],
      "env": {
        "DB_PATH": "${CLAUDE_PLUGIN_ROOT}/data"
      }
    }
  }
}
```

### Claude Desktop

`~/Library/Application Support/Claude/claude_desktop_config.json` (macOS)

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/Users/me/projects"]
    }
  }
}
```

## Building an MCP Server

### Python (FastMCP)

```python
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("my-server")

@mcp.tool()
def search_docs(query: str) -> str:
    """Search internal documentation."""
    return f"Results for: {query}"

if __name__ == "__main__":
    mcp.run()
```

### TypeScript

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new McpServer({ name: "my-server", version: "1.0.0" });

server.tool("search_docs", { query: { type: "string" } }, async ({ query }) => ({
  content: [{ type: "text", text: `Results for: ${query}` }],
}));

const transport = new StdioServerTransport();
await server.connect(transport);
```

## Variable Interpolation

| Variable | Context |
|----------|---------|
| `${env:VAR_NAME}` | Environment variable |
| `${workspaceFolder}` | Cursor workspace root |
| `${CLAUDE_PLUGIN_ROOT}` | Claude Code plugin directory |
| `${CLAUDE_PROJECT_DIR}` | Current project directory |
| `${user_config.*}` | Plugin user configuration |

## Security Best Practices

- Verify server source before installing
- Use least-privilege API keys
- Prefer stdio for local-only tools
- Audit server code for data exfiltration
- Scope filesystem access to required directories
- Never commit secrets in `mcp.json`; use env vars

## Packaging MCP in Plugins

Both Cursor and Claude Code support bundling MCP servers in plugins:

**Cursor**: `mcp.json` at plugin root  
**Claude Code**: `.mcp.json` at plugin root or inline in `plugin.json`

Plugin MCP servers start automatically when the plugin is enabled.

## Deeplinks (Cursor)

Share MCP install links:

```
cursor://anysphere.cursor-deeplink/mcp/install?name=$NAME&config=$BASE64_ENCODED_CONFIG
```

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Server not appearing | Check `mcp.json` syntax; restart client |
| Connection failed | View MCP logs (Cursor: Output panel → MCP Logs) |
| Tool not callable | Verify tool schema; check server permissions |
| Auth errors | Confirm env vars and OAuth config |