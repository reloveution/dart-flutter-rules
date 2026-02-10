---
title: Providers and Scoping
description: Provider types, scope to narrowest subtree
---

# Providers and Scoping

## Provider Types

- **Provider** — exposes a value
- **ChangeNotifierProvider** — exposes listenable; auto-disposal
- **FutureProvider** — exposes Future result
- **StreamProvider** — exposes Stream values
- Use to expose values and manage state within the widget tree.

## Scoping

- Scope each provider to the narrowest subtree that consumes it.
- Don't place providers at app root if only one feature uses them.
- Reduces rebuild scope and keeps dependencies local.
