---
title: Layer Dependencies
description: Dependency chain and interface contracts between layers
---

# Layer Dependencies

## Dependency Chain

All dependencies flow through **constructor interfaces** (abstract classes or interfaces):

```
Controllers → Use Cases → Repositories → DataSources
     ↑            ↑            ↑              ↑
  (via DI)    (via DI)     (via DI)      (raw data)
```

### Rules

1. **Repositories** depend on DataSources/Services through constructor interfaces
2. **Use Cases** depend on Repositories through constructor interfaces
3. **Controllers** (Bloc, Cubit, ViewModel) depend on Use Cases through constructor interfaces
4. **Use Cases** can be shared across different feature controllers
5. **Use Cases** can depend on other Use Cases through constructor interfaces

### Data Flow

- **DataSources** return raw data (JSON, bytes, platform primitives)
- **Repositories** handle parsing and transformation into domain models
- Data parsing is performed in the repository layer only

## Example

```dart
// DataSource: raw
abstract class IApiTodoDts {
  Future<Map<String, dynamic>> fetchRaw();
}

// Repository: parsing, SSOT
abstract class ITodoRepo {
  Future<Result<List<Todo>>> getTodos();
}

class TodoRepoImpl implements ITodoRepo {
  TodoRepoImpl(this._dts);  // Constructor interface
  final IApiTodoDts _dts;

  @override
  Future<Result<List<Todo>>> getTodos() async {
    final raw = await _dts.fetchRaw();
    return Result.ok((raw['items'] as List)
        .map((e) => Todo.fromJson(e as Map<String, dynamic>))
        .toList());
  }
}

// Use Case: can depend on other Use Cases
class GetTodosUcs {
  GetTodosUcs(this._repo, this._authUcs);  // Repo + another Use Case
  final ITodoRepo _repo;
  final GetAuthUserUcs _authUcs;
}
```

## Adjacent Layers Only

- Presentation never reaches Data directly
- Data must not depend on UI code
- Communication only between adjacent layers
