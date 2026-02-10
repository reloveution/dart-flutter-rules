---
title: Firecrawl MCP Server
description: Web scraping, single/batch scrape, map, extract
---

# Firecrawl MCP Server

## When to Use

- Scrape content from pages
- Find documentation, code examples
- Get current internet information

## When NOT to Use

- Symbol search in project code (use Dart MCP)

## Search Status

- **firecrawl_search: UNAVAILABLE (503).**
- Use `web_search` or `firecrawl_map` + `firecrawl_scrape` instead.

## Key Commands

- **scrape** — single page; formats: markdown, html; use maxAge for speed
- **batch_scrape** → **check_batch_status** — multiple URLs
- **map** — discover URLs on site; then scrape needed ones
- **crawl** → **check_crawl_status** — comprehensive site; use with caution (token limits)
- **extract** — structured data with schema/prompt

## Configuration

- FIRECRAWL_API_KEY (required for cloud)
- maxAge for caching (e.g. 172800000 = 2 days)

## Workflow

1. Single page → scrape
2. Multiple URLs → batch_scrape
3. Site discovery → map → scrape/batch_scrape
4. Structured data → extract with schema
