# Claude Code MCP Integration

Source: [code.claude.com/docs/en/mcp](https://code.claude.com/docs/en/mcp)

Connect Claude Code to external tools and data sources via Model Context Protocol.

## Project Configuration

`.mcp.json` in project root:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/dir"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "${env:GITHUB_TOKEN}"
      }
    }
  }
}
```

## Plugin MCP Servers

Bundle in plugins via `.mcp.json` at plugin root:

```json
{
  "mcpServers": {
    "plugin-api": {
      "command": "${CLAUDE_PLUGIN_ROOT}/bin/server",
      "args": ["--port", "8080"],
      "cwd": "${CLAUDE_PLUGIN_ROOT}"
    }
  }
}
```

Plugin MCP servers start automatically when the plugin is enabled.

## Quick Setup

```bash
# Inside Claude Code
/mcp
```

Follow prompts to add, verify, and manage MCP servers.

## Transport Types

| Type | Config |
|------|--------|
| stdio | `command` + `args` |
| SSE | `url` pointing to SSE endpoint |
| HTTP | `url` with streamable HTTP |

## Variable Substitution

| Variable | Description |
|----------|-------------|
| `${CLAUDE_PLUGIN_ROOT}` | Plugin directory |
| `${CLAUDE_PROJECT_DIR}` | Project root |
| `${env:VAR}` | Environment variable |
| `${user_config.*}` | Plugin user config |

## Security

- Project-scope MCP servers require workspace trust approval
- Review server permissions before enabling
- Use least-privilege API keys
- Managed deployments can restrict allowed servers

## Tool Search

For large tool sets, Claude Code supports tool search to load only relevant tools on demand. See the Agent SDK tool search docs.

## Debugging

```bash
/mcp      # List servers and connection status
/doctor   # Diagnose MCP configuration
```

## Related

- `../../standards/mcp.md` — Cross-platform MCP reference
- `../plugins/reference.md` — Plugin MCP schema
- [MCP quickstart](https://code.claude.com/docs/en/mcp-quickstart)