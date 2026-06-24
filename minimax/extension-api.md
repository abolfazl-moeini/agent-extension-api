# MiniMax Extension Development (MCP-Focused)

MiniMax's primary way to extend AI coding agents is through **official MCP servers**.

## MiniMax MCP

MiniMax provides ready-to-use MCP servers (Python and JavaScript) that expose their multimodal capabilities:

- Text-to-Audio / Voice synthesis
- Voice cloning & design
- Music generation
- Text-to-Image
- Image-to-Video / Text-to-Video
- Video task querying
- And more

These MCP servers can be connected to:
- Claude Desktop
- Cursor
- Cherry Studio
- Other MCP-compatible clients (including many AI coding tools)

## Developing with MiniMax Extensions

1. Get a MiniMax API key.
2. Run the official MCP server via `uvx minimax-mcp` (Python) or `npx minimax-mcp-js`.
3. Configure in the client's `mcp.json` or settings (provide API key and base path for outputs).
4. The agent can then use tools like `text_to_audio`, `generate_video`, `text_to_image`, etc.

## Integration Pattern

MiniMax is designed to be "plugged in" to existing AI coding tools (Cursor, Claude Code, Codex, etc.) via MCP.

They also offer Token Plans specifically for using their models inside those coding agents.

## Key Docs in This Collection

| Guide | Path |
|-------|------|
| Model catalog | `minimax/overview.md` |
| MCP servers | `minimax/mcp.md` |
| Shared standards | `standards/mcp.md` |

Run via `uvx minimax-mcp` (Python) or `npx minimax-mcp-js` (JavaScript).
