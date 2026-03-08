---
name: intel-asrai
description: AI-powered web search via x402 micropayments on Base. Returns synthesized answers with cited sources. Each search costs $0.005 USDC from your own wallet. No API keys, no subscriptions — just connect and search.
license: MIT
metadata: {"openclaw":{"emoji":"🔍","requires":{"env":["INTEL_PRIVATE_KEY"]}},"clawdbot":{"emoji":"🔍","requires":{"env":["INTEL_PRIVATE_KEY"]}}}
---

# Intel — AI Web Search via x402

Use `intel_search` when the user asks about current events, recent news, live prices, or anything that requires up-to-date information beyond your training data.

## When to search

- Current events, breaking news, recent developments → search
- Live prices, scores, weather → search
- Research questions needing latest sources → search
- General knowledge you already know well → do NOT search (costs $0.005 USDC each time)

## Tool

```
intel_search(
  query:   string,
  mode:    "speed" | "balanced" | "quality",
  sources: ("web" | "academic" | "discussions")[]
)
```

**mode** — choose based on query type:
- `speed` — current events, simple facts, news
- `balanced` — default for most queries
- `quality` — deep research, complex topics

**sources** — choose based on what the user needs:
- `["web"]` — general results (default)
- `["academic"]` — research papers, studies
- `["discussions"]` — Reddit, forums, community sentiment

## Usage patterns

- "What happened with X today?" → `intel_search(query, mode="speed")`
- "Explain the latest research on X" → `intel_search(query, mode="quality", sources=["academic"])`
- "What are people saying about X?" → `intel_search(query, sources=["discussions"])`

## Output rules

- Lead with the synthesized answer directly — no preamble
- List sources as numbered links after the answer
- For factual questions: direct answer first, then supporting detail
- For news: key developments first, then sources
- Never mention tool names, API calls, or payment details in responses
- Keep it concise — synthesize, don't dump raw results

## Cost

Each search costs **$0.005 USDC** from the user's wallet on Base mainnet. Inform the user if they ask about cost. Payments are signed by the user's own wallet — never a shared key.
