---
name: flutter-performance
description: Performance optimization for Flutter apps. Use when optimizing lists, build methods, const/keys, images, RepaintBoundary, isolates, or profiling with DevTools.
---

# Flutter Performance

## Lists
- `ListView.builder` / `GridView.builder` / `SliverList` for large lists — never `Column`/`Row` with many children
- `const` constructors for list item widgets
- Pagination: load in chunks, combine with builder
- Lazy loading: load on demand (scroll/visibility)

## Build Methods
- No expensive work in `build()` — move to `initState`, `didChangeDependencies`, or cached values
- Scope rebuilds: `Builder`, `ValueListenableBuilder`, `StreamBuilder`, `BlocBuilder`
- Extract frequently rebuilt subtrees into separate widget classes

## Const & Keys
- `const` constructors for static widgets — reused across rebuilds
- Keys for widgets that maintain identity across reorders: `ValueKey`, `ObjectKey`, `UniqueKey`

## Images
- `Image.asset` — cached automatically
- Network images: `cached_network_image` package
- Don't reload same image on every rebuild

## RepaintBoundary
- Wrap complex custom painters — isolates repaint region from siblings/parent
- Adds a compositing layer; profile before/after to validate benefit

## Isolates
- `compute()` for CPU-intensive work: JSON parsing, image processing, batch transforms
- Function and argument must be top-level or static (isolate can't share references)

## Data Structures
- Right structure for the job: List vs Set vs Map, growable vs fixed
- Prefer O(1)/O(log n) over O(n) at scale
- Cache expensive computations when inputs don't change

## Profiling
- Flutter DevTools: Timeline, CPU profiler, memory view
- Identify: build time, layout, paint, rasterize bottlenecks
- Profile before/after optimizations and periodically during development
