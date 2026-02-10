---
title: Core Widget Patterns
description: Composition, build optimization, Container alternatives, context
---

# Widgets for UI

- Everything in Flutter's UI is a widget; compose complex UIs from smaller, reusable widgets
- Prefer composing smaller widgets over extending existing ones
- Create separate widgets instead of methods that return widgets

# Build Method Optimization

- Avoid long methods and complex logic in build methods and onPressed callbacks
- Extract complex logic into separate methods
- Extract string concatenations into dedicated methods

# Immutability

- Widgets (especially StatelessWidget) are immutable
- When UI needs to change, Flutter rebuilds the widget tree

# Never Use Container

- `SizedBox.shrink()` or `SizedBox.expand()` instead of empty Container
- `ColoredBox` instead of Container with only color
- `DecoratedBox` instead of Container with only decoration
- Combine widgets when multiple properties are needed

# Context and Callbacks

- `addPostFrameCallback` — use extremely rarely, only where truly necessary
- Check `context.mounted` before dialogs or context-dependent operations (use_build_context_synchronously)
- Pass callback functions (events or controller methods) to reusable widgets, not state managers
- When injecting via providers: get controllers from DI; in widget tree get from context, not DI
- In dialogs and context changes: pass controller methods, not controllers

# Keys, Theme, Colors

- Use keys for widgets that need to maintain state across rebuilds
- Use proper theme inheritance instead of hardcoded colors
- Use full hex for Flutter colors (8 digits: AARRGGBB)
