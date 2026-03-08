---
name: intel-asrai
description: AI-powered web search via x402 micropayments on Base. Returns synthesized answers with cited sources. Each search costs $0.005 USDC from your own wallet. No API keys, no subscriptions — just connect and search.
license: MIT
---

# Intel — AI Web Search via x402

## Prerequisites

This skill requires **intel-asrai-mcp** connected to your MCP client.

### Install this skill

```bash
npx skills add https://github.com/abuzerasr/intel-asrai-skill -y
```

If the scope prompt blocks install, use:
```bash
npx skills add https://github.com/abuzerasr/intel-asrai-skill -g -y
```

### OpenClaw — Remote URL (recommended)

Edit `~/.openclaw/openclaw.json` and add:

```json
{
  "mcp": {
    "servers": {
      "intel-search": {
        "url": "https://intel-mcp.asrai.me/mcp?key=0x<your_private_key>",
        "transport": "sse"
      }
    }
  }
}
```

OpenClaw watches the file and applies changes automatically — no restart needed.

### OpenClaw — Local npx

Edit `~/.openclaw/openclaw.json` and add:

```json
{
  "mcp": {
    "servers": {
      "intel-search": {
        "command": "npx",
        "args": ["-y", "intel-asrai-mcp"],
        "transport": "stdio",
        "env": { "INTEL_PRIVATE_KEY": "0x<your_private_key>" }
      }
    }
  }
}
```

### Claude Desktop — JSON config

```json
{
  "mcpServers": {
    "intel-search": {
      "command": "npx",
      "args": ["-y", "intel-asrai-mcp"],
      "env": { "INTEL_PRIVATE_KEY": "0x<your_private_key>" }
    }
  }
}
```

Config file location: macOS `~/Library/Application Support/Claude/claude_desktop_config.json`, Windows `%APPDATA%\Claude\claude_desktop_config.json`, Linux `~/.config/Claude/claude_desktop_config.json`.

### n8n / remote connections

- HTTP Streamable: `https://intel-mcp.asrai.me/mcp?key=0x<your_private_key>`
- SSE (legacy): `https://intel-mcp.asrai.me/sse?key=0x<your_private_key>`

### Key via environment variable

Store in `~/.env` and omit from URL/config:
```
INTEL_PRIVATE_KEY=0x<your_private_key>
```

Each search costs **$0.005 USDC** from your wallet on Base mainnet.

## Payment transparency

- Always inform the user of the cost if they ask.
- Payments are signed by the user's own wallet — never a shared key.
- Wallet must have USDC on Base mainnet.

## MCP tools available

| Tool | What it does | Cost |
|---|---|---|
| `intel_search` | AI web search — synthesized answer with cited sources | $0.005 |

## Tool parameters

```
intel_search(
  query:   string,                              // the search query or question
  mode:    "speed" | "balanced" | "quality",    // default: balanced
  sources: ("web" | "academic" | "discussions")[] // default: ["web"]
)
```

## Output rules

- Present the synthesized answer directly — do not show raw JSON.
- Always include sources as a numbered or bulleted list with clickable links.
- If the user asks a factual question, lead with the direct answer, then supporting detail.
- For news queries, summarize key developments first, then cite sources.
- Never mention tool names or API calls in responses.
- Keep responses concise — synthesize, don't dump.

## Usage patterns

- **Current events:** "What happened with X today?" → `intel_search(query, mode="speed")`
- **Research:** "Explain the latest research on X" → `intel_search(query, mode="quality", sources=["academic"])`
- **Community sentiment:** "What are people saying about X?" → `intel_search(query, sources=["discussions"])`

## References

- Endpoint details: `skills/intel-asrai/references/endpoints.md`
- npm: https://www.npmjs.com/package/intel-asrai-mcp
