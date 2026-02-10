---
title: Control Flow and Readability
description: Guard clauses, early returns, boolean expressions
---

# Control Flow and Readability

## Guard Clauses

Use early returns to reduce nesting. Validate preconditions at start:

```dart
// Bad
if (state is Loaded) { /* nested */ }

// Good
if (state is! Loaded) return;
/* main logic at root */
```

Prefer `is!` over `!(x is Type)`.

## Booleans

Don't use `== true` or `== false` with boolean expressions. Use directly.

Exception: `bool?` may need `== true` to distinguish true/false/null.

## Other

- Single-line early returns for simple conditions
- No empty else blocks
- No empty statements
- Use `.isEven` not `% 2 == 0`
- `return value = compute();` when joining return with assignment
