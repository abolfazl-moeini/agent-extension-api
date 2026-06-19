This repository is a curated collection of developer documentation focused on **how to develop extensions, plugins, skills, and tools** for major AI coding agents and platforms.

## Purpose

The goal is to enable an AI coding agent (like you) to:
- Understand the extension/plugin architecture of each tool.
- Generate correct code, manifests, SKILL.md files, MCP servers, hooks, etc.
- Follow the current (2026) best practices and standards.

## Repository Structure

```
<brand>/
  extension-api.md          ← START HERE for each tool (most important)
  <section>/
    index.md or specific guides
```

**Brands** (each has its own extension model):
- `vscode/`
- `cursor/`
- `claude-code/`
- `anthropic/`
- `openai/`
- `xai/`
- `minimax/`

## Current State of AI Coding Tool Extensibility (2026)

Most platforms have converged on a few shared concepts:

### 1. Agent Skills (open standard)
- Defined in a `SKILL.md` file with YAML frontmatter.
- Contains `name`, `description`, instructions, and optional dynamic content.
- Supports `!`command`` for injecting live output.
- Can be user-invoked (`/skill-name`) or auto-discovered by the agent.
- Used by: Cursor, Claude Code, Codex/OpenAI, and others.

### 2. MCP (Model Context Protocol)
- The "USB-C for AI tools".
- Allows agents to connect to external tools, data sources, and capabilities.
- Servers can be local (stdio) or remote (SSE/HTTP).
- Supported (to varying degrees) by Cursor, Claude Code, OpenAI Agents SDK, xAI Grok Build, MiniMax, etc.

### 3. Plugins / Bundles
- A distribution unit that packages Skills + Rules + Agents + MCP servers + Hooks.
- Usually defined by a small manifest (`plugin.json` or similar).
- Can be installed from marketplaces or loaded locally for development.
- Strong implementations: Cursor, Claude Code, Codex.

### 4. Rules / Persistent Instructions
- Project-level or user-level instructions (often `.mdc` or `AGENTS.md` / `CLAUDE.md`).
- Applied automatically or based on globs.

## How to Use This Documentation (Workflow for You)

When asked to create a plugin/extension for a specific tool:

1. **Read the brand's `extension-api.md`** first. This is the synthesized developer guide.
2. Dive into the relevant sections:
   - Skills → how to write effective `SKILL.md`
   - MCP → how to expose tools
   - Plugins → manifest structure and packaging
   - Rules / Agents / Hooks as needed
3. Look for examples (manifest JSON, SKILL.md frontmatter, directory layout).
4. Follow the exact namespacing and file placement rules for that platform.
5. Generate complete, ready-to-test artifacts (directory structure + files).

## Tool-Specific Notes

**VS Code**
- Traditional but very powerful.
- Use `package.json` contribution points + activation events.
- For language features, strongly prefer implementing a Language Server (see LSP guide).
- Key: Extension host isolation (no DOM access).

**Cursor**
- Modern plugin system built on Skills + MCP.
- `extension-api.md` + `plugins/` + `skills/` are critical.
- Plugins are Git-based and go through review for the marketplace.

**Claude Code**
- Very rich plugin model (skills, agents, hooks, MCP, LSP servers inside plugins).
- Detailed quickstart for creating plugins with manifest + skills.
- Strong emphasis on namespacing for plugins (`/plugin-name:skill`).

**Anthropic / Claude**
- Skills are first-class (uploadable via Skills API).
- MCP connector available in the API.
- Plugins are primarily a Claude Code concept but skills are cross-product.

**OpenAI**
- Skills + Agents SDK + MCP are the current direction.
- Assistants API is deprecated — migrate to Responses + tools/skills.
- Codex surfaces have plugin/skill support.

**xAI (Grok)**
- Primarily powerful function calling + tools.
- Growing native + community MCP support.
- Good for exposing custom tools or integrating via MCP into coding agents.

**MiniMax**
- Best integration path is their official MCP servers (multimodal: voice, image, video, music).
- Designed to be dropped into Cursor, Claude Code, etc.
- Token Plans available for using their models inside coding tools.

## Common Pitfalls to Avoid When Generating

- Wrong directory structure for plugins (e.g. putting everything inside `.claude-plugin/`).
- Missing or incorrect frontmatter in `SKILL.md`.
- Forgetting namespacing for plugin skills.
- Using deprecated APIs (OpenAI Assistants, etc.).
- Not providing proper `description` fields (agents rely on them for discovery).
- Ignoring transport options for MCP (stdio vs SSE/HTTP).

## Recommended Output When Creating a Plugin

Provide:
- Complete directory tree.
- All manifest files (`plugin.json`, `.mcp.json`, `hooks.json`, etc.).
- At least one well-written `SKILL.md` with good description and examples.
- Configuration snippets for the target client (Cursor mcp.json, Claude Desktop config, etc.).
- Testing instructions (`--plugin-dir`, reload commands, etc.).

Use the docs in this repo as ground truth for formats and best practices.

---

This context file + the `*/extension-api.md` files should give you (the AI) everything needed to generate high-quality, correct extensions/plugins for these AI coding tools.
