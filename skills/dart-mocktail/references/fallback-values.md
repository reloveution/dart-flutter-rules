---
title: Fallback Values
description: registerFallbackValue for custom types
---

# Fallback Values

## Rule

- Register fallback values for **every non-nullable custom type** you pass through argument matchers.
- Must run before stubbing or verifying.
- Use `registerFallbackValue(SomeType())` — provide a valid instance.

## When

- Before `when()` or `verify()` that use matchers like `any()`, `captureAny()`, `captureThat()` with custom types.
- Typically in `setUpAll()` so it runs once per test file.

## Example

```dart
setUpAll(() {
  registerFallbackValue(MyDomainType());
  registerFallbackValue(Result.success(dummy));
});
```
