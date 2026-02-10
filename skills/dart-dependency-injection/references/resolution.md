---
title: Dependency Resolution
description: Composition root setup example
---

# Dependency Resolution

## Where to Resolve

- Resolve at composition root: `main()` or dependency setup function.
- Pass resolved dependencies to constructors when creating instances.

## Example

```dart
// At composition root (main.dart or setup function)
final service = getIt<IService>();
final repository = getIt<IRepository>(param1: service);
final useCase = getIt<IUseCase>(param1: repository);
final controller = MyController(useCase: useCase); // constructor injection
```

## Chain

- Datasources → Repositories → Use Cases → Controllers.
- Each layer receives its dependencies; no layer fetches from get_it internally.
