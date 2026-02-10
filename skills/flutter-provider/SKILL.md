---
name: flutter-provider
description: Provider state management for Flutter. Use when exposing values with Provider, ChangeNotifierProvider, FutureProvider, StreamProvider, scoping with context.watch/read/select, ProxyProvider, or testing provider-based state.
---

# Flutter Provider

## Overview

Provider family usage, scoped rebuilds, ProxyProvider, lifecycle, and debugging.

## Reference Files

See detailed documentation for each topic:

- [providers-scoping.md](references/providers-scoping.md) - Provider types, scope to narrowest subtree
- [type-safety.md](references/type-safety.md) - Generic type arguments
- [change-notifier-proxy.md](references/change-notifier-proxy.md) - ChangeNotifierProvider, ProxyProvider
- [watch-read-select.md](references/watch-read-select.md) - context.watch, read, select
- [lifecycle.md](references/lifecycle.md) - Create callbacks, outside build
- [provider-value-diagnostics.md](references/provider-value-diagnostics.md) - Provider.value, DevTools
- [incremental-mounting.md](references/incremental-mounting.md) - MultiProvider, many providers
- [value-listenable-migration.md](references/value-listenable-migration.md) - ValueListenableProvider migration
- [testing.md](references/testing.md) - Mock/fake injection

## Quick Reference

| Need | Use |
|------|-----|
| Rebuild on change | context.watch<T>() in build |
| One-off action | context.read<T>() in callbacks |
| Slice of state | context.select<T, R>() or Selector |
| Outside build | didChangeDependencies or callbacks |
| Existing instance | Provider.value |
| Many providers | MultiProvider; consider incremental mounting |
