# OpenAI Assistants API Migration Guide (Deprecated)

Source: https://developers.openai.com (redirect from platform.openai.com/docs/assistants/overview)

**Important:** The Assistants API has been deprecated. It will shut down on August 26, 2026. Migrate to the Responses API.

The fetched content provided a comprehensive migration guide plus extensive current OpenAI developer documentation on the new Responses API, Agents SDK, tools (MCP, Skills, Computer use, etc.).

---

## Summary from Migration Guide

After achieving feature parity in the Responses API, we've deprecated the Assistants API. It will shut down on August 26, 2026. Follow the migration guide to update your integration.

We’re moving from the Assistants API to the new Responses API for a simpler and more flexible mental model.

### Key Changes

| Before       | Now             | Why? |
| ------------ | --------------- | ---- |
| `Assistants` | `Prompts`       | Prompts hold configuration (model, tools, instructions) and are easier to version and update |
| `Threads`    | `Conversations` | Streams of items instead of just messages |
| `Runs`       | `Responses`     | Responses send input items or use a conversation object and receive output items |
| `Run steps`  | `Items`         | Generalized objects |

Full migration examples, request/response comparisons, and code snippets were included in the page content.

The large page also included extensive navigation and documentation for current OpenAI platform capabilities useful for AI coding agent plugin development:

- Agents SDK (define agents, orchestration, guardrails, sandboxes, etc.)
- Tools: Web search, MCP and Connectors, Skills, Shell, Computer use, File search, etc.
- Realtime API
- Many other modern capabilities

For full details, see the original page and related guides on developers.openai.com.

---

*Note: The complete raw markdown from the tool call is very long (full docs navigation + migration details). For plugin generation use cases, prioritize the Responses API + Agents SDK + MCP/Skills sections.*