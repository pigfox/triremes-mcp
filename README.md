# Triremes MCP server

Find out who needs your fix, from inside your AI assistant.

[Triremes](https://triremes.com) lists real problems people keep reporting with the software they use, and business websites with poor SEO / AEO: gaps in what search engines and AI answer engines can read. This is its official, read-only MCP server. Connect it to Claude, Cursor, VS Code or any MCP client and ask in plain words.

- **Endpoint:** `https://triremes.com/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** none
- **Cost to query:** free
- **Official MCP Registry:** `com.triremes/triremes`

## Who it is for

- **SEO and AEO agencies and freelancers** looking for businesses whose websites have measurable gaps, filtered by kind of business, country, city and gap score.
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
| `search_problems` | Problems people keep reporting, biggest first: title, tier, number of reports, last reported, summary, whether it is sold as a lead or an idea report, price and page link | `query`, `kind` (`lead` or `idea_report`), `cursor` |
| `search_website_gaps` | Business websites Triremes measured: kind of business and place, gap score, failed checks by name, date measured, price and page link | `business`, `country` (ISO code, e.g. `US`), `city`, `gap_score` (`poor`, `fair`, `good`), `cursor` |
| `get_website_gap_score` | One website's gap score, what it means, its failed checks, date measured, price and page link | `site_id` (required, e.g. `site-17`) |
| `show_samples` | The free sample lead and sample idea report, so you can see exactly what a buyer gets | none |

## Example prompts

- "Find problems shop owners have with refunds that I could build a fix for."
- "Show me dentists' websites in the US with a poor gap score."
- "What's the gap score of site-17, and which checks does it fail?"
- "Show me the free samples so I know what a lead contains."

## What is free and what is paid

Everything this server returns is free to read. It never returns the paid data: no business names, websites, email addresses or other contact details. Where something is for sale, the answer links to its page on triremes.com, where you can see the price before you buy.

| On triremes.com | Price |
|---|---|
| Browsing problems and websites | Free |
| A problem's leads: every business found to have it, with the email address each published as its own, the page it was published on and a CSV | $19 per business found |
| An idea report, for a problem with no business found yet | $9 (Tier II) or $19 (Tier I) |
| One website with poor SEO / AEO: the business, its website, how to contact it and every finding, with a CSV | $99 |

No subscription; each purchase is one item. All sales are final. Current prices are on the [pricing page](https://triremes.com/pricing).

## What the gap score means

Triremes checks a business's homepage for gaps in what search engines and AI answer engines can read, such as HTTPS, the title, the meta description, structured data, the sitemap, robots.txt and broken links. Each check is weighted by how serious it is (3, 2 or 1). The gap score is the share of the measured checks that the website fails. A check Triremes could not measure, or one with nothing to check, counts neither way.

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
