---
title: Registration Patterns
description: Factory vs singleton
---

# Registration Patterns

## Factory

- Use factory registration for stateless services.
- New instance per resolution.
- Use when instance has no mutable state or can be recreated safely.

## Singleton

- Use singleton for stateful services that need to persist.
- Single instance shared across the app.
- Use for repositories, API clients, databases.

## Prefer Instance-Based Singletons

- Prefer instance-based singletons registered in get_it.
- Avoid static methods and proxy wrappers for backward compatibility.
- Register real instances, not lazy wrappers that hide dependencies.
