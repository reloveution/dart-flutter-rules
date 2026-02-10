---
title: Injection Patterns
description: Constructor injection, bad/good, exceptions
---

# Injection Patterns

## Always Constructor Injection

- Inject all dependencies through constructors.
- Never use service locator calls inside classes.
- Classes receive dependencies as constructor parameters, not fetch internally.

## Interfaces

- Use abstract classes for interfaces, not concrete implementations.
- Enables swapping implementations (e.g. mock in tests).

## Bad vs Good

- **Bad:** `getIt.get<IService>()` inside constructor or method.
- **Good:** `MyClass(this.service, this.repository)` — dependencies passed in.

## Exception

- Rare cases where constructor injection is impractical.
- Example: global audio player for button click sounds.
- Document exceptions clearly; keep to absolute minimum.
