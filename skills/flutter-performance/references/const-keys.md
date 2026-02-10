---
title: Const Constructors and Keys
description: const for static widgets, keys for state
---

# Const Constructors and Keys

## Const Constructors

- Use `const` constructors for static widgets.
- Reduces rebuild overhead; const widgets can be reused.
- Apply to widgets that don't change (labels, icons, static layout).

## Keys

- Use proper keys for widgets that need to maintain identity.
- Helps Flutter preserve state across rebuilds when item order changes.
- `ValueKey`, `ObjectKey`, `UniqueKey` — choose based on identity semantics.
- Optimize widget rebuilds with keys and state management.
