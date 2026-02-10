---
title: Architecture Error Handling
description: Result type, zones, and multi-level protection for business logic
---

# Architecture Error Handling

## Result&lt;T&gt;

Use `Result<T>` for all business logic error handling.

- All services, repositories, use cases, and controllers must communicate through `Result<T>` wrapper
- Never throw exceptions in business logic
- See **dart-error-handling** skill for Result implementation and exception vs Error handling

## Multi-Level Protection

For critical operations (e.g. measurement, scientific data integrity):

1. **Result&lt;T&gt;** – primary error wrapper for all business operations
2. **runZonedGuarded** – wrap critical measurement/calculation zones
3. **try/catch** – additional protection within zones for unexpected failures

### runZonedGuarded

Use for operations where uncaught errors must not propagate:

```dart
runZonedGuarded(() async {
  final result = await measurementService.capture();
  // Critical path - any uncaught error is caught
}, (error, stack) {
  log('Critical measurement error', error: error, stackTrace: stack);
});
```

### Within Zones

Use try/catch inside zones for operations that might fail transiently:

```dart
runZonedGuarded(() async {
  try {
    final result = await repo.getData();
    return result;
  } on TimeoutException catch (e) {
    return Result.failure(NetworkError.from(e));
  }
}, (e, s) => log('Zone error', error: e, stackTrace: s));
```

## Layer Responsibilities

- **Repositories**: Convert exceptions to `Result<T>.failure`
- **Use Cases**: Propagate `Result<T>`, compose repository results
- **Controllers**: Handle `Result<T>` for UI feedback (snackbars, dialogs)
