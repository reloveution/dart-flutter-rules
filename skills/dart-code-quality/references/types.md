---
title: Type Safety and Annotations
description: Avoid dynamic, sealed classes, explicit types
---

# Type Safety and Annotations

## Avoid dynamic

Use proper type annotations.

## Sealed Classes

Use sealed for state management when possible.

## Return Types

Declare return types explicitly. Use `void` not `Null`.

## Type Inference

- Prefer explicit types when inference not obvious
- Avoid types on closure params when inferable
- Setters: never specify return type
- Avoid type names as parameter names

## Patterns

- Pattern matching over `.runtimeType.toString()` or `.toString()` for types
- Prefer int literals over double when possible
- Class modifiers: `sealed`, `base`, `final`, `interface`, `abstract`, `mixin`

## Generics

- Explicit type args when inference would use `dynamic` or reduce clarity
- Typed Command variants over `dynamic` callbacks on public APIs

## Other

- annotate_redeclares for redeclared fields
- avoid_shadowing_type_parameters
- avoid_private_typedef_functions
