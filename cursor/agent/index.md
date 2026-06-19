# Cursor Agent

Source: https://cursor.com/docs/agent

---

Agent is Cursor's assistant that can complete complex coding tasks independently, run terminal commands, and edit code. Access in sidepane with Cmd+I.

## How Agent works

An agent is built on three components:

1. **Instructions**: The system prompt and rules that guide agent behavior
2. **Tools**: File editing, codebase search, terminal execution, and more
3. **Model**: The agent model you pick for the task

Cursor's agent orchestrates these components, tuning for each frontier model.

## Tools

- Semantic search (indexed codebase)
- Search files and folders + exact keywords
- Web search
- Fetch Rules
- Read files (supports images)
- Edit files
- Run shell commands
- Browser control (screenshots, navigation)
- Image generation
- Ask questions (for clarification)

No limit on number of tool calls.

## Checkpoints

Automatic snapshots before major changes. Click to preview and restore files.

## Queued messages

Add follow-ups while Agent is working. They execute after current task.

Use Cmd+Enter for immediate send.

## More

See related docs for Browser tool, Rules, etc.

Full details and videos in source.
