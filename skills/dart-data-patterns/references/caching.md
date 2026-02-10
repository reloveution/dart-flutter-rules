---
title: Caching & Performance
description: Caching strategies, TTL, pagination
---

# Caching & Performance

## Caching Strategies

- Implement proper caching strategies with TTL (time-to-live).
- Define invalidation rules (on write, on time, on demand).
- Cache at appropriate layer (repository, datasource, HTTP client).

## Pagination

- Use pagination for large datasets.
- Support cursor-based or offset-based pagination.
- Lazy load in UI (ListView.builder, infinite scroll).

## Performance

- Avoid loading entire datasets into memory.
- Use background parsing (compute, isolates) for large payloads.
- Minimize serialization/deserialization in hot paths.
