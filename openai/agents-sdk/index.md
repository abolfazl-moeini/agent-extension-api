# OpenAI Agents SDK

Source: [developers.openai.com](https://developers.openai.com)

Build agentic applications with tools, handoffs, guardrails, and MCP support.

## Core Concepts

| Concept | Description |
|---------|-------------|
| **Agent** | LLM with instructions, tools, and guardrails |
| **Tool** | Callable function (built-in, custom, or MCP) |
| **Handoff** | Transfer control between agents |
| **Guardrail** | Input/output validation |
| **Session** | Conversation state management |

## Quick Start (Python)

```python
from agents import Agent, Runner

agent = Agent(
    name="Code Assistant",
    instructions="You help developers write and review code.",
    tools=[...],
)

result = await Runner.run(agent, "Review this function for bugs")
print(result.final_output)
```

## Quick Start (TypeScript)

```typescript
import { Agent, run } from "@openai/agents";

const agent = new Agent({
  name: "Code Assistant",
  instructions: "You help developers write and review code.",
  tools: [...],
});

const result = await run(agent, "Review this function for bugs");
console.log(result.finalOutput);
```

## MCP Integration

Connect external tools via MCP servers:

```python
from agents.mcp import MCPServerStdio

server = MCPServerStdio(
    name="filesystem",
    params={"command": "npx", "args": ["-y", "@modelcontextprotocol/server-filesystem", "/tmp"]},
)

agent = Agent(
    name="File Agent",
    mcp_servers=[server],
)
```

## Built-in Tools

- Web search
- File search
- Computer use
- Shell execution
- Code interpreter
- MCP connectors

## Skills Integration

Load Agent Skills into SDK agents:

- Project skills from `.codex/skills/` or plugin bundles
- Skills provide domain instructions the agent follows
- Combine with custom tools for full capability

## Sandboxed Execution

Agents SDK supports isolated execution environments for:
- Shell commands
- File operations
- Code execution

Configure sandbox policies per agent.

## Related

- `../skills/index.md` — Skill authoring
- `../mcp/index.md` — MCP configuration
- `../extension-api.md` — Extension overview
- `../assistants/migration.md` — Migration from Assistants API