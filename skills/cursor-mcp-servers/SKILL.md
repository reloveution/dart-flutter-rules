---
name: cursor-mcp-servers
description: How to use MCP servers in Cursor. Use when choosing between Dart MCP, Firecrawl, Hugging Face; when running Dart/Flutter tools, web scraping, or ML model search; when add_roots, pub_dev_search, scrape, or analyze_files are needed.
---

# Cursor MCP Servers

## Overview

Usage rules for Dart MCP, Firecrawl MCP, and Hugging Face MCP servers in Cursor. When to use each, priority guidelines, and workflows.

## Reference Files

See detailed documentation for each topic:

- [overview.md](references/overview.md) - General principles, verify before use
- [dart-mcp.md](references/dart-mcp.md) - Dart MCP commands, add_roots, pub, analyze
- [firecrawl-mcp.md](references/firecrawl-mcp.md) - Scrape, map, batch, extract; search unavailable
- [huggingface-mcp.md](references/huggingface-mcp.md) - Models, datasets, papers, image gen
- [priorities.md](references/priorities.md) - Which tool for Dart packages, web, ML
- [usage-rules.md](references/usage-rules.md) - 11 usage rules
- [workflow-examples.md](references/workflow-examples.md) - Key workflow examples
- [errors-limits.md](references/errors-limits.md) - Error handling, limitations per server

## Quick Reference

### Dart MCP First
- Dart/Flutter: add_roots → analyze_files, pub_dev_search, run_tests
- Pub packages: ALWAYS pub_dev_search, never web search

### Firecrawl
- Search UNAVAILABLE (503) — use web_search or map + scrape
- Single page: scrape; multiple: batch_scrape; structured data: extract

### Hugging Face
- ML models, datasets, papers — use HF MCP
- Dart packages — use Dart MCP, not HF
