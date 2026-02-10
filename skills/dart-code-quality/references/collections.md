---
title: Collections and Data Processing
description: Literals, functional methods, equality
---

# Collections and Data Processing

## Literals

Use `[]`, `{}` instead of `List()`, `Map()`.

## Methods

- `.contains()` over `.indexOf() != -1`
- `.isEmpty` / `.isNotEmpty` over `.length == 0` / `.length > 0`
- `.whereType<T>()` over `.where((e) => e is T).cast<T>()`
- Inline in literals; avoid `.add()` / `.addAll()` after creation
- `StringBuffer` for string building in loops

## Data Processing

- Functional: `map`, `where`, `fold` over imperative loops
- `Duration` with milliseconds for consistency
- Cascade operators `..` when appropriate

## Equality

- Override `hashCode` when overriding `==`
- Don't override in mutable classes
- Avoid null checks in equality operators

## Switch

- `.byName()` for enum from string: `ParamType.values.byName(json['type'] as String)`
- Exhaustive cases in switch expressions
- No default on enums when all covered
