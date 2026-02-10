---
title: Build Method Optimization
description: Avoid expensive ops, builders, separate widgets
---

# Build Method Optimization

## Avoid Expensive Operations in build()

- Never do expensive work directly in `build()`.
- Build runs frequently; expensive ops cause jank.
- Move to `initState`, `didChangeDependencies`, or computed/cached values.

## Use Builders

- Use builders when only part of the tree needs to rebuild.
- `Builder`, `ValueListenableBuilder`, `StreamBuilder` scope rebuilds.
- Reduces unnecessary widget tree updates.

## Separate Widgets

- Extract complex or frequently rebuilt parts into separate widgets.
- Lets Flutter skip rebuilding stable ancestors.
- Keeps build methods focused and cheap.
