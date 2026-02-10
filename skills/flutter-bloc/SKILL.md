---
name: flutter-bloc
description: Complete guide for Bloc and Cubit state management in Flutter. Use when implementing bloc/cubit state management, naming events and states, testing blocs with bloc_test, configuring bloc_lint, or choosing between Bloc and Cubit for feature state.
---

# Flutter Bloc

## Overview

Complete guide for Bloc and Cubit state management in Flutter applications.

## Reference Files

See detailed documentation for each topic:

- [naming.md](references/naming.md) - Event and state naming conventions
- [state-modeling.md](references/state-modeling.md) - Equatable, sealed, single-class, props
- [bloc-concepts.md](references/bloc-concepts.md) - Cubit vs Bloc, emit, observers, internal events
- [architecture.md](references/architecture.md) - Layer separation, repository injection, coordination
- [flutter-widgets.md](references/flutter-widgets.md) - BlocBuilder, BlocListener, context.read/watch/select
- [testing.md](references/testing.md) - bloc_test, blocTest, widget test mocking
- [code-quality.md](references/code-quality.md) - bloc_lint, bloc_tools
- [ecosystem.md](references/ecosystem.md) - Packages, event transformers, DevTools

## Quick Start

### Naming

- **Events**: Past tense, `BlocSubject + verb` (e.g. `LoginButtonPressed`)
- **Base event**: `BlocSubjectEvent`
- **States**: Nouns, `BlocSubject + Initial|Success|Failure|InProgress`
- **Base state**: `BlocSubjectState`

### Bloc vs Cubit

| Use Cubit when | Use Bloc when |
|----------------|---------------|
| Simple state, no event traceability | Complex flows, need event history |
| Less boilerplate | Debounce/throttle on events |

### blocTest

```dart
blocTest<CounterCubit, CounterState>(
  'emits [1] when increment is called',
  build: () => CounterCubit(),
  act: (cubit) => cubit.increment(),
  expect: () => [const CounterState(1)],
);
```

## Key Rules

- Do not wrap `emit()` in try-catch
- Inject repositories via constructor
- Coordinate blocs via BlocListener adding events to another bloc
- Use BlocProvider.of(context) in child BuildContext, not provider context
- Handle all states in UI: empty, loading, error, populated

## External Resources

- [bloc package](https://bloclibrary.dev)
- [bloc_test](https://pub.dev/packages/bloc_test)
- [bloc_lint](https://pub.dev/packages/bloc_lint)
