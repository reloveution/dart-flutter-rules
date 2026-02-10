---
title: Variables and Mutability
description: final, ternary over mutable if-else, null init
---

# Variables and Mutability

## Prefer final

Use `final` when value won't change.

## Ternary Over If-Else

```dart
// Bad
int val = x;
if (cond) { val = y; }

// Good
final int val = cond ? y : x;
```

Extract to method for complex conditions.

## Other

- Final params unless mutation needed
- `for (final item in list)`
- `Type? v;` not `Type? v = null;`
