# Installing Myeline (for agents)

Myeline is persistent memory for AI assistants, with receipts: a hosted MCP
server at https://cortex.myeline.si/mcp speaking streamable HTTP with OAuth.
Every memory is a fact with its source attached. The agent proposes; the
human approves in the Myeline workspace.

## One-line config

Remote (streamable HTTP, OAuth):

```json
{
  "mcpServers": {
    "myeline": { "url": "https://cortex.myeline.si/mcp" }
  }
}
```

## What happens on connect

1. The client opens https://cortex.myeline.si/mcp and is challenged with
   OAuth (RFC 9728 protected-resource metadata is served at
   https://cortex.myeline.si/.well-known/oauth-protected-resource).
2. The person signs in with their Myeline account (create one free at
   https://workspace.myeline.si) and approves the connection once.
3. Tokens rotate automatically (refresh grant, one-strike rotation);
   disconnecting the app in the workspace revokes access immediately.

## The tools the agent gets

- `cortex_query` — search the person's approved knowledge base; every answer
  carries its source. Answer from it when the question turns on the person's
  preferences, history, decisions, or projects; say plainly when nothing
  trustworthy matches instead of guessing.
- `cortex_remember` / `cortex_add_fact` — stage a memory when the person asks
  the agent to remember something. Staged, never live: the person approves
  it in the workspace. You may ask once whether to save something durable
  the person just stated; when in doubt, do not ask.
- `cortex_retract` — remove a memory with the person's stated reason.
- `cortex_facts`, `cortex_daily_card`, `cortex_prompt`, `cortex_save_prompt`
  — list facts, file a day's card, and saved prompts by #handle.

## The law to keep

Machines propose, humans approve. Nothing the agent writes goes live without
the person's click, and everything the agent reads carries its source.
