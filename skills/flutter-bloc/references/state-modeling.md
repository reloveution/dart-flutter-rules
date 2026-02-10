---
title: State Modeling
description: Equatable, sealed classes, single-class states, props
---

# State Modeling

## Equatable and Immutability

1. Extend Equatable for all state classes (value equality).
2. Annotate state classes with `@immutable`.
3. Implement `copyWith` for easy state updates.
4. Use const constructors when possible.

## Single-Class vs Sealed

5. **Single concrete class + status enum**: For simple, non-exclusive states or when many properties are shared.
6. In single-class approach: make properties nullable and handle based on current status.
7. **Sealed class + subclasses**: For well-defined, exclusive states.
8. Store shared properties in sealed base; state-specific in subclasses.
9. Use exhaustive switch statements for all state subclasses.

## Choice

10. Prefer sealed for type safety and exhaustiveness; prefer single-class for conciseness and flexibility.

## Equatable Details

11. Pass all relevant properties to `props` getter.
12. Use `List.of` or `Map.of` for List/Map in props to ensure value equality.
13. To retain previous data after error: use single state class with nullable data and error fields.
14. Emit a new instance each time; never reuse the same instance.
