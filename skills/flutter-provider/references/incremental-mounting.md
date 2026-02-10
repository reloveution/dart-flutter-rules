---
title: Incremental Mounting
description: Many providers, deep stacks
---

# Many Providers

- When the application has a very large number of providers, consider incremental mounting.
- Example: mount providers during splash flows as features load.
- Alternative composition to avoid deep MultiProvider stacks at root.

# MultiProvider

- Group multiple providers with MultiProvider to avoid deeply nested declarations.
- Keeps provider tree flat and readable.
- Balance: don't put everything in one MultiProvider if it creates a huge stack.
