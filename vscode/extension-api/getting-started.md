# Your First VS Code Extension

1. Install Yeoman + generator: npm install -g yo generator-code
2. yo code
3. Choose "New Extension (TypeScript)"
4. code .
5. F5 to launch Extension Development Host
6. Run the Hello World command

Key files:
- package.json (contributes, activationEvents)
- src/extension.ts (activate / deactivate)

See the official "Extension Guides" and samples repo for real patterns (webview, tree view, language features, etc.).
