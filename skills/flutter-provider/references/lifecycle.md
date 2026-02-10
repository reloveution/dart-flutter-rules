---
title: Lifecycle and Instantiation
description: Create callbacks, outside build, no external mutable vars
---

# Create/Update Callbacks

- Do not instantiate provider objects from external mutable variables.
- Rely on create/update callbacks so provider can rebuild with fresh dependencies.
- Keeps provider in control of object lifecycle.

# Obtaining Provider Outside Build

- If you need to obtain a provider outside build, use lifecycle-safe points.
- Use `didChangeDependencies` or callbacks (e.g. onPressed, Future.then).
- Do NOT use constructors or initState — context may not be ready or mounted.
