# Language Extensions & Language Server Protocol Overview

Source: https://code.visualstudio.com/api/language-extensions/overview

---

# Language Extensions Overview

VS Code provides smart editing via Language Extensions (not built into core).

Two categories:

## Declarative language features

Defined in config files (TextMate grammars, snippets, language-configuration.json).

Guides:
- Syntax Highlight guide
- Snippet Completion guide  
- Language Configuration guide

## Programmatic language features

Rich dynamic features (completion, diagnostics, hover, definition, formatting, refactoring, etc.).

Can be implemented directly with `vscode.languages.register*Provider` APIs or via Language Server using the Language Server Protocol (LSP).

LSP allows writing one language server that works across editors.

See the dedicated Language Server Extension Guide for full walkthrough with samples.

Special topics: Multi-root workspace support, Embedded languages.

Full list of programmatic features available in the programmatic-language-features page.
