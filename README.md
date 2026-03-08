# intel-asrai-skill

Claude skill for [Intel](https://intel.asrai.me) — AI-powered web search via x402 micropayments on Base.

Installs instructions into Claude so it automatically knows when and how to use Intel web search.

## Install

### OpenClaw (recommended)

> **Note:** This skill is not yet in the ClawHub registry. Use the full GitHub URL:

```bash
npx skills add https://github.com/abuzerasr/intel-asrai-skill
```

Or clone manually:

```bash
git clone https://github.com/abuzerasr/intel-asrai-skill.git ~/.openclaw/skills/intel-asrai
```

### Claude Desktop / other MCP clients

```bash
npx skills add https://github.com/abuzerasr/intel-asrai-skill
```

## What this skill does

- Teaches Claude when to use `intel_search` vs its own knowledge
- Defines how to present results (synthesized answers + sources)
- Sets cost awareness ($0.005 USDC per search)
- Covers all search modes: `speed`, `balanced`, `quality`
- Covers all source types: `web`, `academic`, `discussions`

## Prerequisites

Requires **intel-asrai-mcp** connected to your MCP client.

### OpenClaw — Remote URL (easiest, recommended)

No local install needed. Run:

```bash
openclaw config set mcpServers.intel-search.url "https://intel-mcp.asrai.me/mcp?key=0x<your_private_key>"
```

### OpenClaw — Local npx

```bash
openclaw config set mcpServers.intel-search.command "npx"
openclaw config set mcpServers.intel-search.args '["-y", "intel-asrai-mcp"]'
openclaw config set mcpServers.intel-search.env.INTEL_PRIVATE_KEY "0x<your_private_key>"
```

### Claude Desktop — JSON config

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

Use the hosted MCP server — no install needed:
- HTTP Streamable: `https://intel-mcp.asrai.me/mcp?key=0x<your_private_key>`
- SSE (legacy): `https://intel-mcp.asrai.me/sse?key=0x<your_private_key>`

### Key via environment variable

Store your key in `~/.env` and omit it from the URL/config:

```
INTEL_PRIVATE_KEY=0x<your_private_key>
```

Then use: `https://intel-mcp.asrai.me/mcp`

Your wallet must have USDC on Base mainnet. Each search costs **$0.005 USDC**.

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
