# Myeline

Plug-and-play memory for any AI. Every memory is a single fact with its
source attached. Nothing an AI saves goes live until you approve it in a
human review queue, and removing a fact takes a written reason that stays
in the audit log. One retraction stops a stale fact in every connected
assistant at once.

**Endpoint:** `https://cortex.myeline.si/mcp` (remote MCP, streamable HTTP, OAuth)

**Registry:** [si.myeline/myeline](https://registry.modelcontextprotocol.io/#servers/si.myeline%2Fmyeline) on the official MCP Registry

**Glama:** [![si.myeline/myeline MCP connector](https://glama.ai/mcp/connectors/si.myeline/myeline/badges/score.svg)](https://glama.ai/mcp/connectors/si.myeline/myeline)

**Website:** https://myeline.si · **Docs:** https://workspace.myeline.si/docs

## Connect any MCP client

- **Claude** — Settings → Connectors → Add custom connector → the endpoint above
- **ChatGPT** — Settings → Apps & Connectors → search "Myeline" (official directory listing)
- **Replit** — one click:

[![Add Myeline to Replit](https://replit.com/badge?theme=dark&mcp=eyJkaXNwbGF5TmFtZSI6ICJNeWVsaW5lIiwgImJhc2VVcmwiOiAiaHR0cHM6Ly9jb3J0ZXgubXllbGluZS5zaS9tY3AifQ==)](https://replit.com/integrations?mcp=eyJkaXNwbGF5TmFtZSI6ICJNeWVsaW5lIiwgImJhc2VVcmwiOiAiaHR0cHM6Ly9jb3J0ZXgubXllbGluZS5zaS9tY3AifQ==)

- **Any MCP client** — add a streamable HTTP server at the endpoint and sign in
  with your Myeline account (dynamic client registration supported).

## What it does

- AI clients **propose** memories; they land in a review queue, never straight into memory
- You **approve** or retire each fact; retirement requires a written reason
- Every answer **shows its source**; no match means it says so instead of guessing
- Facts file under `identity:word` tags (person, project, client) and stay consistent
- Free tier: 200 memories. Team brains: $20/seat/month with their own MCP address

By [Sandbox Group LLC](https://github.com/Sandbox-Group-LLC) · Myeline, P.O. Box 40072, Portland, OR 97240

## Slack

Add Myeline to your workspace:

[![Add to Slack](https://platform.slack.com/img/add_to_slack.png)](https://slack.com/oauth/v2/authorize?client_id=10042690022548.12607106906722&scope=channels:history,chat:write,commands,mcp:connect)

Grants channel history (read), writing, slash commands, and MCP connect. Your
team approves every fact before it becomes memory.

## OpenCode

Remote MCP with OAuth — add to `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "myeline": {
      "type": "remote",
      "url": "https://cortex.myeline.si/mcp",
      "enabled": true
    }
  }
}
```

OpenCode detects the OAuth challenge on first use; sign in with your Myeline
account (create one free at [workspace.myeline.si](https://workspace.myeline.si))
and approve once. Your agent can then search your approved facts before
answering and stage new memories for your review.
