---
name: flutter-performance
description: Performance optimization for Flutter apps. Use when optimizing lists (ListView.builder), build methods, const constructors, isolates (compute), RepaintBoundary, images, pagination, or profiling with DevTools.
---

# Flutter Performance

## Overview

Performance rules: lists, build methods, const/keys, images, RepaintBoundary, isolates, data structures, profiling.

## Reference Files

See detailed documentation for each topic:

- [lists.md](references/lists.md) - ListView.builder, recycling, pagination, lazy loading
- [build-methods.md](references/build-methods.md) - Avoid expensive ops, builders, separate widgets
- [const-keys.md](references/const-keys.md) - const constructors, keys
- [images.md](references/images.md) - Image caching
- [repaint-boundary.md](references/repaint-boundary.md) - RepaintBoundary for custom painters
- [isolates.md](references/isolates.md) - compute() for CPU-intensive work
- [data-algorithms.md](references/data-algorithms.md) - Efficient structures and algorithms
- [profiling.md](references/profiling.md) - Flutter DevTools

## Quick Reference

- **Lists:** ListView.builder, const items, pagination, lazy load
- **Build:** No expensive ops; builders; separate widgets
- **Const/Keys:** const for static; keys for identity
- **Isolates:** compute() for CPU-heavy work
- **RepaintBoundary:** Complex custom painters
- **Profile:** Flutter DevTools regularly
