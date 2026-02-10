---
title: Provider.value and Diagnostics
description: Existing instances, DevTools
---

# Provider.value

- Any object can be exposed as state.
- Prefer `Provider.value` for existing instances managed by StatefulWidgets.
- Use when you create the object elsewhere and pass it down.

# Diagnostics

- Register diagnostic information (toString, DiagnosticableTreeMixin) on provided objects.
- Improves Flutter DevTools readability.
- Helps when debugging provider state in the inspector.
