---
title: Testing
description: Provider wiring, mock/fake injection
---

# Testing Providers

- Ensure provider wiring is shallow and focused in tests.
- Prefer injecting mock/fake dependencies through providers configured per test case.
- Override providers in test widget tree to inject test doubles.
- Keep test setup minimal; scope providers to what each test needs.
