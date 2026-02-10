---
title: ChangeNotifier and ProxyProvider
description: ChangeNotifierProvider, ProxyProvider variants
---

# ChangeNotifierProvider

- Prefer when the provided object needs automatic disposal by the widget tree.
- Use ChangeNotifierProxyProvider when the object depends on other providers.
- Disposes the notifier when the provider is removed from the tree.

# ProxyProvider

- Build objects that depend on other providers using ProxyProvider variants.
- Dependencies refresh when upstream values change.
- ProxyProvider, ChangeNotifierProxyProvider, etc.
