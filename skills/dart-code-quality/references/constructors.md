---
title: Constructors and Initialization
description: Initializing formals, super params, factory
---

# Constructors and Initialization

## Initializing Formals

Prefer `this.field` over assignments in constructor body.

## Super Parameters

```dart
// Before
Child(this.field) : super(field: field);

// After
Child(super.field);
```

## Late

Use `late` for non-null variables initialized after construction.

## Factory

Use factory constructors for complex object creation.

## Assert

Place asserts in initializer list when possible. Always provide messages.

## Avoid

- Field initializers in const classes
- Unused constructor parameters
