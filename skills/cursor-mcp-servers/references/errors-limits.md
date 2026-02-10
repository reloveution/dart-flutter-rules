---
title: Error Handling and Limitations
description: Per-server errors and limits
---

# Error Handling and Limitations

## Dart MCP

**Errors:** Verify SDK; DTD needs new URI after loss; use dart_fix for analysis; check network for pub

**Limits:** DTD requires running app; large projects take time

## Firecrawl

**Search 503:** firecrawl_search unavailable — web_search or map + scrape

**Errors:** onlyMainContent for scrape errors; maxAge for speed; batch_scrape for multiple URLs

**Limits:** Crawl can overflow tokens; limit depth and pages; JS-heavy sites may fail

## Hugging Face

**Errors:** hf_whoami for auth; repo ID format `author/name`; specify repo_type if auto-detect fails

**Limits:** 100 models/datasets per query; 10 repos per hub_repo_details; Flux 1 Schnell only; large docs need offset

## Performance

- Firecrawl: maxAge for caching; limit results
- HF: concise_only for papers; batch hub_repo_details; filter early (author, task, library)
- HF image: defaults for speed; increase steps only if needed
