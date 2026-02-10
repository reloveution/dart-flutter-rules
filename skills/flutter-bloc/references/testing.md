---
title: Bloc Testing
description: bloc_test, blocTest, mocking in widget tests
---

# Bloc Testing

## Setup

1. Add `test` and `bloc_test` to dev dependencies.
2. Create dedicated test file per bloc: e.g. `counter_bloc_test.dart`.
3. Import `test` and `bloc_test`.

## Test Structure

4. Use `setUp` to initialize bloc; `tearDown` to clean up.
5. Organize tests into groups for shared setup/teardown.
6. Test bloc's initial state before testing transitions.

## blocTest

7. Use `blocTest` for state transition tests.
8. Assert expected sequence of emitted states for each event.

```dart
blocTest<CounterCubit, CounterState>(
  'emits [1] when increment is called',
  build: () => CounterCubit(),
  act: (cubit) => cubit.increment(),
  expect: () => [const CounterState(1)],
);
```

## Widget Tests

9. Mock cubits/blocs in widget tests to verify UI for all possible states.

## Best Practices

10. Keep tests concise, focused, maintainable.
11. Consider bloc_lint in CI/CD pipeline.
