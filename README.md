# intel-asrai-skill

Skill for [Intel](https://intel.asrai.me) — AI-powered web search via x402 micropayments on Base.

Works with **OpenClaw**, **Claude Desktop**, and any MCP-compatible agent. Teaches the agent when and how to use Intel web search, how to present results, and manages cost awareness.

## Install

### OpenClaw

> **Note:** This skill is not yet in the ClawHub registry. Use the full GitHub URL:

```bash
npx skills add https://github.com/abuzerasr/intel-asrai-skill -y
```

If the scope prompt blocks install:

```bash
npx skills add https://github.com/abuzerasr/intel-asrai-skill -g -y
```

Or clone manually into your OpenClaw workspace:

```bash
git clone https://github.com/abuzerasr/intel-asrai-skill.git ~/.openclaw/workspace/skills/intel-asrai
```

### Claude Desktop / other agents

```bash
npx skills add https://github.com/abuzerasr/intel-asrai-skill -y
```

After installing, ask your agent to "refresh skills" or restart the gateway.

## What this skill does

- Teaches the agent when to use `intel_search` vs its own knowledge
- Defines how to present results (synthesized answers + sources)
- Sets cost awareness ($0.005 USDC per search)
- Covers all search modes: `speed`, `balanced`, `quality`
- Covers all source types: `web`, `academic`, `discussions`

## Prerequisites

Requires **intel-asrai-mcp** connected to your agent. Set `INTEL_PRIVATE_KEY` in your environment.

Your wallet must have USDC on Base mainnet. Each search costs **$0.005 USDC**.

---

## MCP Setup

### OpenClaw — Remote URL (easiest, recommended)

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

### Claude Desktop

Add to your Claude Desktop config file:

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

Config file location:
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`
- Linux: `~/.config/Claude/claude_desktop_config.json`

### n8n / remote connections

- HTTP Streamable: `https://intel-mcp.asrai.me/mcp?key=0x<your_private_key>`
- SSE (legacy): `https://intel-mcp.asrai.me/sse?key=0x<your_private_key>`

### Key via environment variable

Store in `~/.env` and omit from URL/config:

```
INTEL_PRIVATE_KEY=0x<your_private_key>
```

Then use: `https://intel-mcp.asrai.me/mcp`

---

## MCP tool

| Tool | Description | Cost |
|---|---|---|
| `intel_search` | AI web search with synthesized answer and cited sources | $0.005 |

**Parameters:**
- `query` — the search question or topic
- `mode` — `speed` \| `balanced` \| `quality` (default: `balanced`)
- `sources` — `["web"]` \| `["academic"]` \| `["discussions"]` (default: `["web"]`)

## Links

- Landing page: [intel.asrai.me](https://intel.asrai.me)
- MCP package: [npmjs.com/package/intel-asrai-mcp](https://www.npmjs.com/package/intel-asrai-mcp)
- GitHub: [github.com/abuzerasr/intel-asrai-skill](https://github.com/abuzerasr/intel-asrai-skill)
- x402 protocol: [x402.org](https://x402.org)

## License

MIT
