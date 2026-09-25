<p align="center"><img src="https://hiasynth.co/hicone-app-light.png" width="96" alt="Hiasynth Humanity"></p>

# Hiasynth Humanity

### Query humanity.

**Europe's population layer.** Demographic, spending and market data for every place in Europe, as one remote MCP server, for your AI assistant or inside your own product.

Nobody could say what a Lyon neighbourhood spends on restaurants, or how many renting families in Bavaria earn above the median. Statistics come as national averages, surveys as small samples, and nothing ties who people are to where they live and what they spend. Hiasynth Humanity models it: all 522 million Europeans, each in a household, each household in its neighbourhood, with a line-by-line budget. That's ~700 attributes per person, queryable in any combination, at any resolution down to 1 km². No real person is in it, so it's private by design.

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=hiasynth&config=eyJ1cmwiOiJodHRwczovL21jcC5oaWFzeW50aC5jbyJ9)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=hiasynth&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.hiasynth.co%22%7D)
[![Install in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install_Server-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=hiasynth&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.hiasynth.co%22%7D&quality=insiders)

```
https://mcp.hiasynth.co
```

Streamable HTTP · OAuth 2.1 (sign in with your Hiasynth account) or an API key · every tool read-only.

## Connect

| Client | How |
|---|---|
| **Claude** (web, desktop, mobile) | Settings → Connectors → Add custom connector → paste the address. [Guide](https://hiasynth.co/docs/connect-claude) |
| **ChatGPT** | Settings → Apps → Create → paste the address. [Guide](https://hiasynth.co/docs/connect-chatgpt) |
| **Claude Code** | `claude mcp add --transport http hiasynth https://mcp.hiasynth.co` [Guide](https://hiasynth.co/docs/connect-claude-code) |
| **Cursor / VS Code** | The buttons above. |
| **Gemini CLI** | `gemini extensions install https://github.com/hi-synth/hiasynth-mcp-server` |
| **Anything else** | Remote MCP over streamable HTTP. [Guide](https://hiasynth.co/docs/connect-any) |

Headless clients send an API key from [hiasynth.co/app/mcp](https://hiasynth.co/app/mcp) as `Authorization: Bearer …`:

```json
{
  "mcpServers": {
    "hiasynth": {
      "url": "https://mcp.hiasynth.co",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

## Build it into your product

The same server is an API for your features and agents: size a market inside a CRM and show where to dig next, tie a marketing tool's personas to the actual population, or show the wallet size of any neighbourhood.

- **Auth:** OAuth 2.1 for user-facing apps, or a server-side API key from [hiasynth.co/app/mcp](https://hiasynth.co/app/mcp) (`Authorization: Bearer …`).
- **Responses:** structured JSON with the numbers already computed: counts, shares, lift against the local baseline, top places, and a confidence tier. Aggregates only, never individual records.
- **Fine control:** `query_population` takes a structured spec (group-by, filters, count/share/avg) for pipelines that need exact shapes.
- **Any MCP client library** works: the official SDKs, the Claude and OpenAI APIs' MCP connectors, LangChain, or plain JSON-RPC over HTTPS.

What `analyze_market` returns for *renting families with above-median income in Bavaria* (trimmed):

```json
{
  "headline": "418,921 households (6.81% of Bayern). Biggest markets: München, Nürnberg.",
  "segment_size": { "count": 418921, "share_pct": 6.81, "population": 6153349 },
  "core_markets": [
    { "name": "München, Landeshauptstadt", "count": 43674, "local_share_pct": 6.51, "lift": 0.96 },
    { "name": "Würzburg", "count": 5272, "local_share_pct": 8.41, "lift": 1.23 }
  ],
  "hotspots": [
    { "name": "Sonthofen, St", "count": 1111, "local_share_pct": 10.56, "lift": 1.5 }
  ],
  "confidence_tier": "medium",
  "computed": "3 attribute filter(s) over 6,153,349 households at municipality resolution; counted, not estimated"
}
```

Full reference: [Build with Hiasynth](https://hiasynth.co/docs/build).

## Try asking

- *How many renting families with above-median income live in Bavaria, and where do they cluster?*
- *What do households in La Croix-Rousse, Lyon, spend on restaurants and cafés?*
- *Who lives in Södermalm, Stockholm — and how is it different from the rest of Sweden?*
- *Which media channels reach women aged 25–40 in the top income quartile in France?*
- *Compare Munich, Hamburg and Vienna for affluent 30–45 year olds.*
- *What does a typical household in Porto spend on eating out, and how does its carbon footprint compare?*

## Tools

| Tool | What it answers |
|---|---|
| `analyze_market` | How many people match a segment, who they are, and where they cluster. |
| `describe_area` | Who lives in a place — demographics, values, economics, media, spending, footprint. |
| `reach_audience` | Which channels, values and brands over-index for a segment. |
| `compare_places` | Side-by-side comparison of places for one segment. |
| `rank_places` | Rank regions or towns for a segment. |
| `sample_persona` | Representative personas (statistical composites, never a real row). |
| `resolve_place` | Turn a name, code, postcode or point into the exact area used. |
| `query_population` | Structured group-by for agent builders. |
| `list_attributes` | Search the attribute catalogue. |

All tools are read-only (`readOnlyHint: true`), return aggregates only, and suppress any cell under the privacy floor. Special-category attributes are never broken down below region level.

## Links

[Docs](https://hiasynth.co/docs/mcp-server) · [Pricing](https://hiasynth.co/docs/pricing) · [Privacy](https://hiasynth.co/privacy) · [Terms](https://hiasynth.co/terms) · [Support](https://hiasynth.co/docs/support)

This repository holds the public listing files (registry `server.json`, Gemini CLI extension). The server itself is operated by Hiasynth AB.
