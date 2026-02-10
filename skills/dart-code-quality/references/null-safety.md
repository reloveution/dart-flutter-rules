---
title: Null Safety
description: Avoid !, extract nullable locals, null-aware operators
---

# Null Safety

## Avoid Force Unwrap

Avoid `!` unless value is guaranteed non-null. Extract nullable values to avoid repeated `!`:

```dart
// Bad
if (state.fractureSystem != null && state.fractureSystem!.uid != current) { }

// Good
final fs = state.fractureSystem;
if (fs != null && fs.uid != current) { }
```

## Operators

- Prefer `?.` and `??` over explicit if-null checks
- Use `??` instead of `if (x == null) return y; return x;`
- Use `??=` instead of `if (x == null) x = y;`
- Use `x ?? defaultValue` not `x ?? null`
- Use `if (x != null)` not `if (x)` for nullable→bool

## Equality

Avoid null checks in equality operators; use null-aware operators.
