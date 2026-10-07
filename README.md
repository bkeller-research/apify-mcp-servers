# Apify-hosted remote MCP servers

Five data tools published by `brenton8907` on Apify are available as hosted,
streamable-HTTP MCP servers. Each directory contains the corresponding
`server.json` for the [official MCP Registry](https://registry.modelcontextprotocol.io/)
under the `io.github.bkeller-research` namespace.

| Server | What it returns | Apify page |
|---|---|---|
| Google Ads Transparency Center | Ads found by advertiser domain or brand, including creatives and available metadata | [Open](https://apify.com/brenton8907/google-ads-transparency-center) |
| PDF Text, Table and OCR Extractor | Per-page text, table rows, Markdown, metadata and OCR | [Open](https://apify.com/brenton8907/pdf-text-table-ocr-extractor) |
| Prediction Markets Data | Kalshi and Polymarket prices, orderbooks, trades and settled results | [Open](https://apify.com/brenton8907/prediction-markets-data) |
| Product Hunt Data | Launches, votes, makers, topics and comments from the official API | [Open](https://apify.com/brenton8907/product-hunt-data) |
| Telegram Channel Scraper | Public channel posts, views, reactions, media and subscriber counts | [Open](https://apify.com/brenton8907/telegram-channel-scraper) |

## Connect

Use the endpoint for the tool you need:

```text
https://mcp.apify.com/?tools=brenton8907/<actor-name>
```

For example:

```text
https://mcp.apify.com/?tools=brenton8907/google-ads-transparency-center
```

The gateway requires Apify OAuth or an Apify API token. Usage is billed by
Apify under each Actor's published pay-per-event prices; review the Actor page
before running it.

## Publishing

GitHub Actions validates and publishes every `server.json` to the official MCP
Registry with GitHub OIDC on changes to `main`. Existing immutable versions are
skipped; metadata changes use a new semantic version.

A weekly `schedule` run acts as a heartbeat, so a pipeline that has stopped
working turns red without needing a commit to notice.

GitHub OIDC only grants the `io.github.<repo-owner>` namespace, so the server
names must match whoever owns this repository. This repository moved from
`brenton-keller` to `bkeller-research` on 2026-09-21 while the names still said
`brenton-keller`, and every publish failed with HTTP 403 for 16 days without a
single red run, because push events were not starting runs at all. The names
were corrected on 2026-10-07. A preflight step now compares every server name
against `github.repository_owner` and fails with a readable message, so the
next ownership change cannot repeat this silently.

### The 2026-10-07 namespace migration

The registry enforces globally-unique remote URLs, so the pre-move
`io.github.brenton-keller/*` entries held the `mcp.apify.com` URLs the new names
needed and blocked them with HTTP 400. Setting those entries to `deprecated` did
**not** release the URLs; only `deleted` did. All seven old versions across the
five servers were therefore deleted, and the five
`io.github.bkeller-research/*` servers were published in their place. The old
names no longer resolve.
