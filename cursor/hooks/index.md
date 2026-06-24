# Cursor Plugin Hooks

Source: [cursor.com/docs/plugins](https://cursor.com/docs/plugins)

Hooks are automation scripts bundled in plugins that respond to agent and workspace events.

## workspaceOpen Hook

The primary documented hook. Returns plugin paths to load when a workspace opens. Useful when the set of plugins depends on the workspace itself.

```bash
#!/bin/bash
# hooks/workspace-open.sh
# Return plugin paths as JSON array
echo '["/path/to/workspace-specific-plugin"]'
```

Register in the plugin manifest or hooks configuration.

## Use Cases

- Load different plugins based on project type (monorepo vs single app)
- Activate MCP servers only for specific workspaces
- Inject workspace-specific rules dynamically

## Related

- `../plugins/creating.md` — Plugin scaffolding with hooks
- `../plugins/reference.md` — Full manifest schema