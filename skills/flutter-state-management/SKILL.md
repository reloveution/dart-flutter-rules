---
name: flutter-state-management
description: State management for Flutter. Use when choosing patterns, implementing BLoC/Cubit, built-in (Streams, Futures, ValueNotifier), ChangeNotifier, or Provider.
---

# Flutter State Management

## Overview

Immutable state, separation of ephemeral vs app state, BLoC/Cubit, built-in solutions, ChangeNotifier, Provider.

## Reference Files

- [general.md](references/general.md) - Separation, immutability, lifecycle, persistence
- [bloc-cubit.md](references/bloc-cubit.md) - BLoC, Cubit, anti-patterns
- [built-in.md](references/built-in.md) - Streams, Futures, ValueNotifier
- [change-notifier-provider.md](references/change-notifier-provider.md) - ChangeNotifier, Provider, MVVM

## Quick Reference

- **General:** Ephemeral vs app state; immutable + copyWith; no globals; single approach per widget
- **BLoC:** Events from UI; no try-catch on emit
- **Cubit:** Public methods; no events in cubit
- **Built-in:** Streams, Futures, ValueNotifier — use when explicitly requested
- **ChangeNotifier/Provider:** Scope narrow; Consumer deep; notifyListeners after mutation
