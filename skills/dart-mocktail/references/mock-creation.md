---
title: Mock Creation
description: Extend Mock, no overrides
---

# Mock Creation

## Rule

- Create mocks by extending `Mock`.
- Never add manual overrides or concrete implementations to the subclass.
- The mock is generated; you only stub and verify.

## Example

```dart
class MockIRepository extends Mock implements IRepository {}
```

## Bad

- Overriding methods in the mock subclass with real logic.
- Adding `@override` implementations beyond what Mock provides.
