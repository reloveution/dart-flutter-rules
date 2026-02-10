---
title: context.watch, read, select
description: When to use each access pattern
---

# context.watch<T>()

- Use when the widget must rebuild in response to changes.
- Call inside build method.
- Subscribes to provider; rebuilds when value changes.

# context.read<T>()

- Use for one-off actions without subscribing.
- Callbacks, event handlers, initState.
- Does not trigger rebuilds; use when you need current value but don't listen.

# context.select<T, R>()

- Use to listen to specific slices of state.
- Minimizes rebuild scope; rebuilds only when selected value changes.
- Selector/Consumer widgets — same idea; place Consumers as deep in the tree as practical.
