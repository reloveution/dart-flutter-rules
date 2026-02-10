---
title: Flutter Bloc Widgets
description: BlocBuilder, BlocListener, BlocSelector, context.read/watch/select
---

# Flutter Bloc Widgets

## Core Widgets

1. **BlocBuilder** – Rebuilds on bloc/cubit state changes; builder must be pure.
2. **BlocListener** – Side effects (navigation, dialogs) in response to state changes.
3. **BlocConsumer** – Combines BlocBuilder and BlocListener.
4. **BlocSelector** – Rebuilds only when selected part of state changes.

## Providers

5. **BlocProvider** – Provides blocs to widget subtrees.
6. **MultiBlocProvider** – Multiple blocs; avoids deep nesting.
7. **RepositoryProvider** – Provides repositories/services.
8. **MultiRepositoryProvider** – Multiple repositories; avoids nesting.

## Context Access

9. `context.read<T>()` – One-off access (callbacks); no rebuild on change.
10. `context.watch<T>()` – Rebuild on change; use inside build.
11. `context.select<T, R>()` – Rebuild when selected slice changes.

## Best Practices

12. Avoid `context.watch` or `context.select` at root of build (unnecessary rebuilds).
13. Prefer BlocBuilder and BlocSelector over context.watch/select for explicit scope.
14. Use Builder to scope rebuilds when using context.watch/select for multiple blocs.

## UI State Handling

15. Handle all possible states explicitly: empty, loading, error, populated.
