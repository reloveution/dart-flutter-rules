---
title: Code Organization
description: Polymorphism over conditionals, coordination focus, maintainable structure
---

# Code Organization

## Polymorphism Over Conditionals

Excessive if-else/switch-case logic indicates poor architecture and creates maintenance issues.

### Rules

- Minimize conditional logic in favor of polymorphism and design patterns
- Use object methods or factories instead of multiple conditional statements
- Group related logic into separate methods and classes
- Keep main classes focused on coordination rather than implementation details

### Example: Polymorphic vs Switch

When all cases call the same method with the same parameters, use the base interface directly:

```dart
// Bad: redundant switch with type casting
IParam _updateParam(IParam param, IParamValue newValue, String changedBy) {
  switch (param.paramType) {
    case ParamType.text:
      final textParam = param as TextParam;
      return textParam.copyWith(
        changeHistory: textParam.changeHistory.addChange(
          newValue as TextParamValue, changedBy,
        ),
      );
    case ParamType.integer:
      final intParam = param as IntegerParam;
      return intParam.copyWith(
        changeHistory: intParam.changeHistory.addChange(
          newValue as IntegerParamValue, changedBy,
        ),
      );
    // ...
  }
}

// Good: polymorphic approach
IParam _updateParam(IParam param, IParamValue newValue, String changedBy) =>
    param.copyWith(
      changeHistory: param.changeHistory.addChange(newValue, changedBy),
    );
```

### Coordination vs Implementation

Main classes should coordinate; implementation details belong in smaller units:

- **Coordination**: Orchestrate calls, pass data, handle flow
- **Implementation**: Actual logic, transformations, algorithms

Extract complex branches into dedicated classes or methods. Use factories for object creation based on type or condition.

## Separation

Implement proper separation between domain, data, and presentation layers. Adhere to maintainable code structure and separation of concerns. UI logic should be separate from business logic.
