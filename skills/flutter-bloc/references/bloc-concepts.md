---
title: Bloc Concepts
description: Cubit vs Bloc, emit, events, observers, internal events
---

# Bloc Concepts

## Cubit vs Bloc

1. Use **Cubit** for simple state management without events.
2. Use **Bloc** for complex, event-driven state management.
3. Prefer Cubit for simplicity; prefer Bloc for traceability and advanced event handling.
4. If unsure, start with Cubit and refactor to Bloc as requirements grow.

## Initial State and Emit

5. Define initial state by passing it to superclass (both Cubit and Bloc).
6. Only use `emit` inside Cubit or Bloc; never externally.
7. Do not wrap `emit` in try-catch; method is safe.
8. Duplicate states (`state == nextState`) are ignored; no rebuild.

## Observers

9. Override `onChange` in Cubit or Bloc to observe state changes.
10. Use custom `BlocObserver` for global observation of all changes and errors.
11. Override `onError` in both Cubit/Bloc and BlocObserver for error handling.
12. Initialize BlocObserver in main.dart for debugging and logging.

## Bloc-Specific

13. Add events in response to user actions or lifecycle events.
14. Use `onTransition` in Bloc to observe full transition (event, current state, next state).
15. Use event transformers (debounce, throttle) for advanced processing.
16. Internal events: private, only for real-time updates from repositories.
17. Use custom event transformers for internal events if needed.

## API Exposure

18. Cubit public methods: only trigger state changes, return `void` or `Future<void>`.
19. Bloc: avoid custom public methods; use `add` for state changes.
20. UI listens to state changes; updates only in response to new states.
21. Keep business logic out of UI; interact via events or public methods only.

## Context

22. Use `BlocProvider.of(context)` within a **child** BuildContext, not the same context where bloc was provided.
