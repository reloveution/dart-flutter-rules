---
title: Usage Rules
description: 11 rules for MCP usage
---

# Usage Rules

1. **Verify availability** — Check tool availability before use
2. **Right tool** — Don't use web search when specialized tool exists
3. **Dart packages** — ALWAYS Dart MCP pub_dev_search
4. **ML/AI** — ALWAYS Hugging Face MCP for models, datasets, papers
5. **Workspace** — Call add_roots before workspace-dependent Dart commands
6. **Optimize** — Use limit, tokens to constrain results
7. **Caching** — Use maxAge in Firecrawl for repeated requests
8. **Sequence** — add_roots → analyze_files; batch_scrape → check_batch_status
9. **Fallback** — If tool unavailable, use alternative
10. **Firecrawl search** — Unavailable; use web_search or map + scrape
11. **HF auth** — Verify hf_whoami if permission errors
