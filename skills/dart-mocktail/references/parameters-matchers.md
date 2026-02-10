---
title: Parameters and Matchers
description: Named params, any(), captureAny, captureThat
---

# Parameters and Matchers

## Named Parameters

- Supply all named parameters in both stubs and verifies.
- Use `any(named: 'param')` when the exact value is irrelevant.
- Omission can cause unexpected match failures.

## Argument Matchers

- `any()` — match any value; use for positional params you don't inspect.
- `captureAny()` — capture argument for later assertion.
- `captureThat(matcher)` — capture when matcher matches.
- Rely on `any()` for positional parameters you don't need to inspect.
