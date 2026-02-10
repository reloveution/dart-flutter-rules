---
title: List Performance
description: ListView.builder, recycling, pagination, lazy loading
---

# List Performance

## ListView.builder

- Use `ListView.builder` for large lists instead of Column/Row with many children.
- Builder creates items lazily; only visible items are built.
- Same for `SliverList`, `GridView.builder`.

## Item Recycling

- Implement proper list item recycling.
- Use `const` constructors where possible for list item widgets.
- Reduces memory and rebuild cost.

## Pagination

- Implement proper pagination for large datasets.
- Load data in chunks; don't fetch entire dataset upfront.
- Combine with ListView.builder for efficient display.

## Lazy Loading

- Implement lazy loading for large datasets.
- Load on demand (scroll, visibility, or user action).
- Keeps initial load fast and memory bounded.
