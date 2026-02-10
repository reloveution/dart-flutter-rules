---
title: Polymorphism Over Type Checking
description: Base interface vs switch/case, bad/good example
---

# Polymorphism Over Type Checking

## Prefer Polymorphism

- Prefer polymorphism through base interfaces over switch/case when all implementations share common behavior.
- If all cases in a switch call the same method with the same parameters, use the base interface method directly.
- Avoid unnecessary type casting (`as`) when the base interface provides the needed functionality.
- Let the type system enforce correctness at compile time.

## Bad (Redundant Switch)

```dart
IParam _updateParam(IParam param, IParamValue newValue, String changedBy) {
  switch (param.paramType) {
    case ParamType.text:
      final textParam = param as TextParam;
      return textParam.copyWith(
        changeHistory: textParam.changeHistory.addChange(
          newValue as TextParamValue, changedBy),
      );
    case ParamType.integer:
      final intParam = param as IntegerParam;
      return intParam.copyWith(
        changeHistory: intParam.changeHistory.addChange(
          newValue as IntegerParamValue, changedBy),
      );
    case ParamType.decimal:
      final decParam = param as DecimalParam;
      return decParam.copyWith(
        changeHistory: decParam.changeHistory.addChange(
          newValue as DecimalParamValue, changedBy),
      );
  }
}
```

## Good (Polymorphic)

```dart
IParam _updateParam(IParam param, IParamValue newValue, String changedBy) =>
    param.copyWith(
      changeHistory: param.changeHistory.addChange(newValue, changedBy),
    );
```

## Benefits

- Eliminates boilerplate; type safety via generics/interface
- Automatically works with new implementations
- Concrete types preserved at runtime
- More maintainable and less error-prone

## When to Use

- When all type-specific cases perform identical operations using methods from the base interface.
- When behavior truly varies by type, switch/pattern matching may still be appropriate.
