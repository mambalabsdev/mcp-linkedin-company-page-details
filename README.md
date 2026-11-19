# LinkedIn Company Page Details MCP Server

[![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-linkedin-company-page-details/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-linkedin-company-page-details) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-linkedin-company-page-details%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-linkedin-company-page-details&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-linkedin-company-page-details)](https://www.npmjs.com/package/@mambalabsdev/mcp-linkedin-company-page-details) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-linkedin-company-page-details)](https://www.npmjs.com/package/@mambalabsdev/mcp-linkedin-company-page-details) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-linkedin-company-page-details)](https://github.com/mambalabsdev/mcp-linkedin-company-page-details/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-linkedin-company-page-details)

An MCP server for the Mamba Labs LinkedIn Company Page Details actor on Apify. LinkedIn company pages as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes LinkedIn company URLs or slugs and returns one row per company with industry, size band, employees on LinkedIn, followers, website, headquarters, type, founded, specialties, About text, similar companies, and recent posts.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-linkedin-company-page-details": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-linkedin-company-page-details"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `get_linkedin_company_details` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Get the LinkedIn company details for Stripe and HubSpot."
- "How many employees does Notion list on LinkedIn, and what is its size band?"

## Tool

`get_linkedin_company_details`. One tool. Example arguments:

```json
{
  "companies": [
    "stripe"
  ]
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `companies` | array | no | LinkedIn company page URLs (https://www.linkedin.com/company/stripe), or slugs (stripe). Showcase pages work too. Numeric company IDs are not readable without a login and come back as free rows. Each company is read once per run. From Clay, wrap a column in a one item list. |
| `include_similar_pages` | boolean | no | yes (default) adds the similar companies LinkedIn shows, as a JSON list. Free; no extra request. |
| `include_recent_posts` | boolean | no | yes (default) adds the recent posts the public page shows, as a JSON list of url, date, text, and likes. Free; no extra request. |
| `max_companies` | number | no | Optional. Read at most this many companies from the list. Default and maximum 5000. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Free rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `company-row`, one company page read | $0.0032 | $0.00304 | $0.00288 | $0.00272 |
| `apify-actor-start`, per run start | $0.006 | $0.006 | $0.006 | $0.006 |

Pages that are missing or blocked, and refused input, are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/linkedin-company-page-details](https://apify.com/mambalabs/linkedin-company-page-details)

## License

MIT. See [LICENSE](LICENSE).
