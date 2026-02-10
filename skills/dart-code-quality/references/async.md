---
title: Async and Await
description: Future, Stream, unawaited, async pass-through
---

# Async and Await

## Prefer async/await

Always use async/await instead of `.then()`. Use `Future` and `Stream` appropriately.

## Avoid Blocking UI

Use async/await for I/O; consider isolates for CPU-intensive tasks.

## Pass-Through

Don't use async/await for simple Future pass-through:

```dart
// Bad
Future<T> method() async { return await other(); }

// Good
Future<T> method() => other();
```

Use async/await only when processing results, handling errors, or doing extra work.

## Avoid Unnecessary

- Omit `async` when await is not used
- Use `return future;` not `return await future;` (unless error handling needs it)
- Use `Future<void>` for async members that don't yield a value

## Unawaited Futures

- Handle Future results explicitly
- Use `unawaited()` for fire-and-forget; never silently discard
- Avoid unnecessary `unawaited()` when not truly fire-and-forget

## Lint

Avoid slow async I/O in critical sections (avoid_slow_async_io).
