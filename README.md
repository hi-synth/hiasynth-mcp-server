<p align="center"><img src="https://hiasynth.co/hicone-app-light.png" width="96" alt="Hiasynth"></p>

# Hiasynth MCP server

**A 1:1 synthetic population of Europe — 522 million people, ~700 attributes each, down to municipality and 1 km² — as a remote MCP server.**

Ask your AI assistant who lives somewhere, how many people match a segment, where they cluster, what they spend on and how to reach them. Every answer is computed from joint distributions over the whole population, with lift against a matched baseline, not recalled from national averages.

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

## Try asking

- *How many households in Bavaria have an electric car and children, and which towns over-index?*
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
