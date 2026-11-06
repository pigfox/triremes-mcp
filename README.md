# Triremes MCP server

[![M8ven Score](https://m8ven.ai/badge/mcp/pigfox-triremes-mcp-89233b?v=9f34a3b22f91aae4175c658dbcaa2a9d)](https://m8ven.ai/mcp/pigfox-triremes-mcp-89233b?s=readme)

Find out who needs your fix, from inside your AI assistant.

[Triremes](https://triremes.com) lists real problems people keep reporting with the software they use, and business websites with poor SEO / AEO: gaps in what search engines and AI answer engines can read. This is its official, read-only MCP server. Connect it to Claude, Cursor, VS Code or any MCP client and ask in plain words.

- **Endpoint:** `https://triremes.com/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** none
- **Cost to query:** free
- **Version:** 1.1.0
- **Official MCP Registry:** `com.triremes/triremes`

## Who it is for

- **SEO and AEO agencies and freelancers** looking for businesses whose websites have measurable gaps, filtered by kind of business, country, city and SEO score.
- **Developers and founders** looking for a problem worth building for, with the number of reports and how recent they are.
- **Anyone selling a fix** who wants to see who has the problem before reaching out.

## Connect

### Claude Code

```sh
claude mcp add --transport http triremes https://triremes.com/mcp
```

### Claude Desktop, Cursor, VS Code and other clients

Add a remote (HTTP) server with this URL:

```json
{
  "mcpServers": {
    "triremes": {
      "url": "https://triremes.com/mcp"
    }
  }
}
```

The exact settings file differs by client; see your client's documentation for remote MCP servers.

## Tools

| Tool | What it returns | Inputs (all optional unless noted) |
|---|---|---|
| `search_problems` | Problems people keep reporting, biggest first: title, tier, how many reports and when the first and last were, the day Triremes listed it, summary, whether it is sold as a lead or an idea report, price, how many times a lead has been sold and when it last was, and its page | `query`, `kind` (`lead` or `idea_report`), `max_sold`, `cursor` |
| `search_website_gaps` | Business websites Triremes measured, each sold on its own: kind of business and place, SEO score and its label, the SEO checks it failed by name, AEO score and the AEO checks it failed, when it was measured, price, how many times it has been sold and when it last was, and its page | `business`, `country` (two-letter ISO code, e.g. `US`), `city`, `gap_score` (an SEO score band: `no-gaps`, `lightly-flawed`, `flawed`, `badly-flawed`, `catastrophic`; or a 10% step: `0`, `1-10` ... `91-100`), `max_sold`, `cursor` |
| `get_website_gap_score` | One website by its id: its SEO score and label, the checks it failed by name, when it was measured, its price, how many times it has been sold and the time of each sale, and its page | `site_id` (required, as `search_website_gaps` gives it) |
| `show_samples` | The free samples: a lead, an idea report and a website with poor SEO / AEO, exactly as a buyer gets them, with links to every problem and every website on sale | none |

A website still being measured says so (`being_measured`): it has no price yet, and can be bought once it has its score.

## Example prompts

- "Find problems shop owners have with refunds that I could build a fix for."
- "Show me dentists' websites in the US with a flawed SEO score."
- "Find roofers' websites in Texas and tell me which AEO checks they fail."
- "Show me the free samples so I know what a lead contains."

## What is free and what is paid

Everything this server returns is free to read. It never returns the paid data: no business names, websites, email addresses or other contact details. Where something is for sale, the answer links to its page on triremes.com, where you can see the price before you buy.

| On triremes.com | Price |
|---|---|
| Browsing problems and websites | Free |
| A problem's leads: every business found to have it, with the address each published as its own, the page it was published on and a CSV | $19 per business found, at least $19 |
| An idea report, for a problem with no business found yet | $19 (Tier I · Proven) or $9 (Tier II · Emerging) |
| One website with poor SEO / AEO: the business, its website, how to contact it and every finding, with a CSV | $99 |

No subscription; each purchase is one item. All sales are final. Current prices are on the [pricing page](https://triremes.com/pricing).

## What the scores mean

- **SEO score:** the share of Triremes' checks of what search engines can read on this homepage that it fails, weighted by how serious each check is. 0% means no gaps; higher is worse.
- **AEO score (sometimes called GEO):** the share of Triremes' checks of whether AI answer engines can reach, read and trust this site that it fails, weighted by how serious each check is. 0% means no gaps; higher is worse.

## Limits

The server is rate-limited per client and overall, so one busy agent cannot crowd out others. Over a limit, a call gets an error asking it to retry after a minute, never a partial answer.

## Links

- Website: <https://triremes.com>
- Pricing: <https://triremes.com/pricing>
- Samples: <https://triremes.com/samples>
- REST API: <https://triremes.com/api/openapi.json>
- Contact: <https://triremes.com/contact>

Triremes is owned and operated by [Pigfox LLC](https://pigfox.com).

This repository holds the server's documentation and its registry entry (`server.json`). The server itself runs at `https://triremes.com/mcp`.
