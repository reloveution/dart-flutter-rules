---
title: Service Location & Container
description: get_it, composition root, resolution order
---

# Service Location & Container

## Container

- Use get_it as dependency injection container.
- Register dependencies in a dedicated setup function or main.

## Composition Root

- **Important:** get_it only at composition root (app initialization).
- Never call `getIt.get<T>()` inside classes.
- Exception: rare documented cases (e.g. global audio player for UI feedback).
- Resolve and pass dependencies into constructors when creating instances.

## Resolution Order

- Register in proper order: datasources → repositories → use cases → controllers.
- Respect dependency graph: register leaf nodes first, then their dependents.
- Resolve dependencies at composition root and pass to constructors.
