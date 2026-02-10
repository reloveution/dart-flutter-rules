---
title: Type Safety
description: Generic type arguments
---

# Type Safety

## Always Specify Generic Type

- Use generic type argument with Provider, Consumer, context.watch, context.read, context.select.
- Examples: `Provider<MyModel>`, `context.watch<MyModel>()`, `context.read<MyModel>()`, `context.select<MyModel, R>()`.
- Retains static type-safety and avoids runtime cast errors.
