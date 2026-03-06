# intel-asrai-skill

Claude skill for [Intel](https://intel.asrai.me) — AI-powered web search via x402 micropayments on Base.

Installs instructions into Claude so it automatically knows when and how to use Intel web search.

## Install

```bash
npx skills add intel-asrai
```

Via Clawhub:

```bash
clawdhub install intel-asrai
```

Manual:

```bash
git clone https://github.com/abuzerasr/intel-asrai-skill.git ~/.openclaw/skills/intel-asrai
```

## What this skill does

- Teaches Claude when to use `intel_search` vs its own knowledge
- Defines how to present results (synthesized answers + sources)
- Sets cost awareness ($0.005 USDC per search)
- Covers all search modes: `speed`, `balanced`, `quality`
- Covers all source types: `web`, `academic`, `discussions`

## Prerequisites

Requires **intel-asrai-mcp** connected to your MCP client. Add to your config:

```json
{
  "mcpServers": {
    "intel-search": {
      "url": "https://intel-mcp.asrai.me/mcp?key=0x<your_private_key>"
    }
  }
}
```

Or set your key once in `~/.env`:

```
INTEL_PRIVATE_KEY=0x<your_private_key>
```

Then use the URL without a key:

```json
{
  "mcpServers": {
    "intel-search": {
      "url": "https://intel-mcp.asrai.me/mcp"
    }
  }
}
```

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
