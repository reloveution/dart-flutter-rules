---
name: dart-data-patterns
description: Data handling patterns for Dart/Flutter applications. Use when implementing data transformation, serialization, caching, layer separation, data flow, DTOs, repositories, offline-first, migrations, and data validation.
---

# Dart Data Patterns

## Overview

Data handling patterns for Dart/Flutter applications: data flow, DTOs, serialization, caching, synchronization, and layer separation.

## Reference Files

See detailed documentation for each topic:

- [data-flow.md](references/data-flow.md) - Repositories, single source of truth, abstractions
- [serialization.md](references/serialization.md) - DTOs, fromJson/toJson, validation
- [streaming.md](references/streaming.md) - Real-time data updates
- [caching.md](references/caching.md) - TTL, pagination, performance
- [synchronization.md](references/synchronization.md) - Local/remote sync, optimistic updates
- [data-management.md](references/data-management.md) - Migrations, modeling, compression
- [security-reliability.md](references/security-reliability.md) - Encryption, backup
- [architecture.md](references/architecture.md) - Domain vs DTO, layer boundaries

## Quick Reference

### Data Flow
- Repositories = single source of truth
- Abstract data sources via interfaces
- Expose immutable data to consumers

### DTOs & Serialization
- DTOs between layers; `fromJson`/`toJson`
- Data classes with `copyWith`
- Validate at boundaries

### Sync
- Optimistic updates; reconcile with backend response
- Offline-first: local persistence + remote sync in repo

### Architecture
- Domain entities: no DB knowledge
- DTOs encapsulate mapping; tables reference DTOs, not converters
