# Model Context Protocol (MCP) | Cursor Docs

Source: https://cursor.com/docs/mcp

# Model Context Protocol (MCP)

## What is MCP?

MCP enables Cursor to connect to external tools and data sources.

### Why use MCP?

Instead of explaining your project structure repeatedly, integrate directly with your tools.

Write MCP servers in any language.

## How it works

Cursor supports three transport methods:

- stdio (local)
- SSE (local/remote)
- Streamable HTTP (local/remote)

Supported capabilities: Tools, Prompts, Resources, Roots, Elicitation, MCP Apps (UI).

## Installing MCP servers

- One-click from Cursor Marketplace or cursor.directory
- Configure with `.cursor/mcp.json` (project) or `~/.cursor/mcp.json` (global)

Example configs for stdio and remote servers provided.

Static OAuth, config interpolation with ${env:...}, ${workspaceFolder} etc.

## Using MCP in chat

Cursor discovers and offers MCP tools. Approval flow, images as context supported.

## Security considerations

Verify sources, review permissions, use least-privilege keys, audit code.

## Real-world examples

Xcode integration, web dev with Linear/Figma, etc.

## FAQ and troubleshooting

See logs in Output panel > MCP Logs, toggles in Settings, etc.

---

## Sitemap

[Overview of all docs pages](/llms.txt)
