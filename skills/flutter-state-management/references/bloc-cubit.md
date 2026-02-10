---
title: BLoC and Cubit Patterns
description: Events, methods, anti-patterns
---

# BLoC Pattern

- Prefer triggering bloc changes by adding events from UI callbacks
  - Example: `() => bloc.add(FormSubmitted(user))`
- If a feature strictly requires public bloc methods as a facade: document that choice; keep event creation inside those methods only
- Do not wrap emit() calls in try-catch; emit() is already safe

# Cubit Pattern

- Interact with cubits via their public methods (e.g. cubit.loadData())
- Keep event classes out of the cubit layer
- Encapsulate business logic inside cubit methods; each method emits the correct state
- Avoid mixing bloc-style events into cubits to preserve clear separation

# What Not to Do

- Don't generate events directly from view — use bloc methods
- Don't wrap emit() in try-catch
- Don't mix BlocBuilder with setState in the same widget
- Don't use setState inside BLoC/Cubit
- Don't mix different state management approaches in the same widget
