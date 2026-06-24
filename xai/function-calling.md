# xAI Function Calling & Tools

Source: [docs.x.ai](https://docs.x.ai)

Extend Grok with custom tools via the Responses API function calling.

## Overview

Grok supports tool use where the model decides when to invoke your tools and provides structured arguments. Built-in tools include web search, image generation, and vision.

## Custom Tool Definition

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_XAI_API_KEY",
    base_url="https://api.x.ai/v1",
)

response = client.responses.create(
    model="grok-4",
    input="What's the weather in San Francisco?",
    tools=[
        {
            "type": "function",
            "name": "get_weather",
            "description": "Get current weather for a location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                        "description": "City name"
                    },
                    "unit": {
                        "type": "string",
                        "enum": ["celsius", "fahrenheit"]
                    }
                },
                "required": ["location"]
            }
        }
    ],
)
```

## Tool Execution Loop

1. Send request with tool definitions
2. Model returns tool call with arguments
3. Execute tool in your application
4. Send tool result back to model
5. Model generates final response

```python
# After receiving tool_call from model
tool_result = get_weather(location="San Francisco", unit="celsius")

response = client.responses.create(
    model="grok-4",
    input=[
        {"role": "user", "content": "What's the weather in San Francisco?"},
        {"role": "assistant", "tool_calls": [...]},
        {"role": "tool", "tool_call_id": "...", "content": str(tool_result)},
    ],
)
```

## Built-in Tools

| Tool | Description |
|------|-------------|
| Web search | Real-time web information |
| Image generation | Create images from text |
| Vision | Analyze image inputs |
| Structured outputs | JSON schema responses |

## Best Practices

- Write clear `description` fields — the model uses them to decide when to call
- Define precise parameter schemas with `required` fields
- Handle tool errors gracefully; return error messages to the model
- Use structured outputs when you need typed responses

## Grok Build Integration

Grok Build CLI is an agentic coding tool. Custom tools and MCP servers extend its capabilities for multi-step workflows.

## Related

- `mcp.md` — MCP server integration
- `overview.md` — xAI API quickstart
- `extension-api.md` — Extension overview