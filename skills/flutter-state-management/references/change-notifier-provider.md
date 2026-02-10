---
title: ChangeNotifier and Provider
description: ChangeNotifier, Provider, MVVM, DI
---

# ChangeNotifier Pattern

- Place shared ChangeNotifier instances above all widgets that consume them
- Keep mutable fields private; expose getters or unmodifiable views
- Invoke notifyListeners() after each state mutation
- Scope ChangeNotifierProvider to the subtree that needs the model
- Use Consumer<T> around the smallest subtree that depends on state; keep unrelated children in Consumer.child
- Call Provider.of<T>(context, listen: false) for imperative actions that should not trigger rebuilds
- Compose multiple providers with MultiProvider when several models are required
- Structure widget trees to minimise rebuild cost: Consumers deep in tree; favour StatelessWidget
- Write focused unit tests for ChangeNotifier classes

# Other Built-in Options

- **ChangeNotifier:** For state more complex or shared across widgets
- **ListenableBuilder:** Listen to ChangeNotifier or other Listenable
- **MVVM:** Use when a more robust solution is needed
- **Dependency Injection:** Manual constructor injection for explicit dependencies
- **Provider:** Use only when explicitly requested; defaults against third-party packages
