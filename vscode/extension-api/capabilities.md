# Extension Capabilities Overview | Visual Studio Code Extension API

Source: https://code.visualstudio.com/api/extension-capabilities/overview

---

# Extension Capabilities Overview

Visual Studio Code offers many ways for extensions to extend its capabilities. It can sometimes be hard to find the right Contribution Points and VS Code API to use. This topic splits extension capabilities into a few categories.

## Common Capabilities

Core pieces of functionality usable in any extension:

- Registering commands, configurations, keybindings, or context menu items.
- Storing workspace or global data.
- Displaying notification messages.
- Using Quick Pick.
- File picker.
- Progress API.

## Theming

Controls look of VS Code (colors of source code and UI).

Extension Ideas: color themes, file icon themes, product icon themes.

## Declarative Language Features

Basic text editing support (syntax highlighting, snippets, bracket matching, auto-indent) defined in configuration files. See:

- Syntax Highlight guide
- Snippet Completion guide
- Language Configuration guide

## Programmatic Language Features

Rich features: hovers, go to definition, diagnostics, IntelliSense, CodeLens, etc. via `vscode.languages.*` API or Language Server.

## Workbench Extensions

Extend UI: TreeView, Webview, custom editors, views, status bar, etc.

## Debugging

Debugger extensions via Debug Adapter Protocol.

## UX Guidelines & Restrictions

- No DOM access
- No custom stylesheets (use provided APIs)

See full details and extension ideas in the source page.
