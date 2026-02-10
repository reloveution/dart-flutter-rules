---
title: Performance
description: Lists, isolates, RepaintBoundary
---

# List Performance

- ListView.builder or SliverList for long lists (lazy-loaded)

# Isolates

- Use compute() for expensive calculations (e.g. JSON parsing) to avoid blocking UI thread

# RepaintBoundary

- Use for expensive custom painters
