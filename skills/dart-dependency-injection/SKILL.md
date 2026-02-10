---
name: dart-dependency-injection
description: Dependency injection patterns for Dart/Flutter applications. Use when configuring get_it, registering dependencies, using constructor injection, setting up composition root, and testing with mocks.
---

# Dart Dependency Injection

## Overview

Dependency injection with get_it: service location at composition root, constructor injection, proper registration order, and testability.

## Reference Files

See detailed documentation for each topic:

- [service-location.md](references/service-location.md) - get_it, composition root only, resolution order
- [registration.md](references/registration.md) - Factory vs singleton
- [injection.md](references/injection.md) - Constructor injection, bad/good, exceptions
- [resolution.md](references/resolution.md) - Composition root setup example
- [management.md](references/management.md) - Lifecycle, scoping, circular dependencies
- [testing.md](references/testing.md) - Mocks, multiple environments

## Quick Reference

### Composition Root Only
- Call `getIt.get<T>()` only at app init (main/setup)
- Never inside class constructors or methods (except rare documented exceptions)

### Constructor Injection
- Inject via constructors: `MyClass(this.service, this.repository)`
- Use abstract interfaces, not concrete implementations

### Registration Order
- datasources → repositories → use cases → controllers

### Testing
- Constructor injection enables easy mocking: `MyClass(mockService, mockRepository)`
