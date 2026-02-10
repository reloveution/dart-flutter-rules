---
title: Data Synchronization
description: Local/remote sync, optimistic updates, offline-first
---

# Data Synchronization

## Local and Remote

- Handle synchronization between local and remote sources.
- Decide: last-write-wins, merge strategies, conflict resolution.

## Optimistic Updates

- Apply optimistic updates when latency allows.
- Reconcile repository state with final backend response.
- Roll back or merge on failure.
- Provide immediate UI feedback; sync in background.

## Offline-First

- Combine local persistence with remote synchronization.
- Implement inside repositories.
- Serve from local cache first; sync when online.
- Queue writes when offline; flush when connected.
