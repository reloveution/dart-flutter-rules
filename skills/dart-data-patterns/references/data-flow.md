---
title: Data Flow
description: Repositories, single source of truth, data abstraction
---

# Data Flow

## Single Source of Truth

- Repositories operate as the single source of truth.
- Reconcile local caches and remote services.
- Expose immutable data to consumers.

## Data Structures

- Define data structures (classes) to represent application data.

## Data Abstraction

- Abstract data sources (API calls, database operations) using Repositories/Services.
- Promotes testability: inject mock implementations.
- Consumers depend on abstractions, not concrete implementations.
