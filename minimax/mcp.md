# MiniMax MCP Servers

Source: [platform.minimaxi.com](https://platform.minimaxi.com)

MiniMax provides official MCP servers exposing multimodal capabilities to any MCP-compatible coding agent.

## Available Capabilities

| Tool Category | Examples |
|---------------|----------|
| Text-to-Audio | Voice synthesis, voice cloning |
| Music | Music generation, cover versions |
| Image | Text-to-image, image editing |
| Video | Text-to-video, image-to-video, task querying |

## Installation

### Python

```bash
uvx minimax-mcp
```

### JavaScript

```bash
npx minimax-mcp-js
```

## Configuration

### Cursor (`.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "minimax": {
      "command": "uvx",
      "args": ["minimax-mcp"],
      "env": {
        "MINIMAX_API_KEY": "${env:MINIMAX_API_KEY}",
        "MINIMAX_API_HOST": "https://api.minimaxi.com",
        "MINIMAX_MCP_BASE_PATH": "/path/to/output"
      }
    }
  }
}
```

### Claude Desktop

```json
{
  "mcpServers": {
    "minimax": {
      "command": "uvx",
      "args": ["minimax-mcp"],
      "env": {
        "MINIMAX_API_KEY": "your-api-key",
        "MINIMAX_MCP_BASE_PATH": "/Users/me/minimax-output"
      }
    }
  }
}
```

### Claude Code (`.mcp.json`)

```json
{
  "mcpServers": {
    "minimax": {
      "command": "uvx",
      "args": ["minimax-mcp"],
      "env": {
        "MINIMAX_API_KEY": "${env:MINIMAX_API_KEY}",
        "MINIMAX_MCP_BASE_PATH": "${CLAUDE_PROJECT_DIR}/minimax-output"
      }
    }
  }
}
```

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `MINIMAX_API_KEY` | Yes | API key from MiniMax platform |
| `MINIMAX_API_HOST` | No | API endpoint (default: `https://api.minimaxi.com`) |
| `MINIMAX_MCP_BASE_PATH` | Yes | Directory for generated files (audio, images, video) |
| `MINIMAX_API_RESOURCE_MODE` | No | Resource handling mode |

## Example Agent Prompts

Once configured, agents can use tools like:

- "Generate a voice narration for this README"
- "Create a product demo video from this screenshot"
- "Generate background music for this presentation"

## Token Plans

MiniMax offers Token Plans for using their models inside coding tools like Cursor and Claude Code. Configure model endpoints separately from MCP tools.

## Related

- `overview.md` — MiniMax model catalog
- `extension-api.md` — Extension overview
- `../../standards/mcp.md` — MCP reference