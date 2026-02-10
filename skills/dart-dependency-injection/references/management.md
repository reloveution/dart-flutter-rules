---
title: Dependency Management
description: Lifecycle, scoping, circular dependencies
---

# Dependency Management

## Lifecycle

- Implement proper dependency lifecycle management.
- Singleton lives for app lifetime; factory creates per resolution.
- Dispose singletons that hold resources if needed (e.g. database, StreamController).

## Scoping

- Use proper scoping for different types of dependencies.
- Global singletons for app-wide services.
- Consider scoped providers (e.g. RepositoryProvider) for feature-specific dependencies in Flutter.

## Circular Dependencies

- Avoid circular dependencies between services.
- If A depends on B and B on A, refactor: extract shared interface, introduce mediator, or split responsibility.
- Circular registration causes runtime errors or infinite loops.
