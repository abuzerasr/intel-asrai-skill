# Intel x402 Endpoints

## Base URL
`https://intel.asrai.me`

## Payment
x402 automatic — $0.005 USDC per request on Base mainnet

## Endpoint

### Search
`POST /search`

**Request body:**
```json
{
  "query":   "your search query",
  "mode":    "balanced",
  "sources": ["web"]
}
```

**Parameters:**
- `query` (required) — the search question or topic
- `mode` (optional) — `speed` | `balanced` | `quality` (default: `balanced`)
- `sources` (optional) — array of `web`, `academic`, `discussions` (default: `["web"]`)

**Response:**
```json
{
  "message": "synthesized answer text",
  "sources": [
    { "title": "Source Title", "url": "https://..." }
  ]
}
```

## Health check
`GET /health` — returns `{ "status": "ok" }`
