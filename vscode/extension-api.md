# VS Code Extension API (Developer Documentation)

This is the official way to develop extensions and language support for VS Code.

## Main Areas

- **Extension API**: Core capabilities for commands, UI, webviews, tree views, configuration, etc.
- **Contribution Points**: Declarative contributions in `package.json` (commands, menus, views, themes, etc.).
- **Language Extensions**: Declarative (grammars, snippets, language config) + Programmatic (via `vscode.languages.*` providers).
- **Language Server Protocol (LSP)**: Recommended way for full-featured language support. Separate client (VS Code extension) + server process.

## Key Resources in This Collection

- `vscode/extension-api/overview.md`
- `vscode/extension-api/capabilities.md`
- `vscode/extension-api/extension-guides.md`
- `vscode/extension-api/getting-started.md`
- `vscode/language-server-protocol/overview.md`
- `vscode/language-server-protocol/guide.md` (detailed LSP sample walkthrough)

## Getting Started as a Plugin/Extension Developer

1. Use the official generator (`yo code`).
2. Study the Extension Guides for real patterns (Webview, TreeView, Custom Editors, Tasks, SCM, Testing, etc.).
3. For language features, prefer LSP when possible (see the LSP guide).
4. Follow UX Guidelines and respect extension host restrictions (no direct DOM access).

Full reference:
- VS Code API (vscode.* namespace)
- Contribution Points
- Activation events

This directory (`vscode/extension-api/`) contains the core developer documentation for building VS Code extensions.
