---
title: Async Design
description: Future-first API design for controllers, use cases, repositories, and datasources
---

# Async Design

## Rule

Write all methods in controllers, use cases, repositories, and datasources as `Future` from the start to avoid rewriting interfaces when async is needed later.

Only keep truly synchronous operations synchronous.

## Why

- Adding `async` to an existing sync method forces all callers to change
- Future-first keeps interfaces stable when I/O is introduced
- Prevents cascade refactors across layers

## Applies To

- **Controllers** (Bloc, Cubit, ViewModel) – methods that trigger data loading
- **Use Cases** – business logic that may call repositories
- **Repositories** – data access (network, database)
- **Datasources** – raw data fetch; repositories handle parsing

## Example

```dart
// Good: Future from the start
abstract class ITodoRepo {
  Future<Result<List<Todo>>> getTodos();
  Future<Result<void>> addTodo(Todo todo);
}

// Avoid: sync initially, then adding Future later
abstract class ITodoRepo {
  List<Todo> getTodos();  // Forces rewrite when we add network
}
```

## Truly Synchronous

Keep synchronous when:
- Pure computation with no I/O
- In-memory transformations
- Getters that return already-loaded data
- Simple validation without external calls
