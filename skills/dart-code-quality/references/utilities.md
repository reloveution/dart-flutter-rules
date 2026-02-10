---
title: Utilities and Validation
description: Getters, enum byName, validation checks
---

# Utilities

## Getters

Use getters instead of parameterless methods for object properties.

## Enum Parsing

Use `.byName()` for enum from string. No intermediate variable if used once:

```dart
// Bad
case 'text': return TextParam.fromJson(json);

// Good
switch (ParamType.values.byName(json['type'] as String)) {
  case ParamType.text: return TextParam.fromJson(json);
}
```

# Validation

- Avoid recursive getters (stack overflow)
- Avoid no-op on primitives
- Check URI existence before using
- Avoid null checks on nullable type params
- Avoid null closures
- Validate environment variable usage (do_not_use_environment)
