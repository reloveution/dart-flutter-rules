---
name: dart-mocktail
description: Mocktail testing guidelines for Dart/Flutter. Use when creating mocks, fakes, stubbing async/sync, verifying interactions, registerFallbackValue, or avoiding MissingStub errors.
---

# Dart Mocktail

## Overview

Mocktail usage: Fake vs Mock, mock creation, fallback values, stubbing, verification, matchers.

## Reference Files

See detailed documentation for each topic:

- [fake-vs-mock.md](references/fake-vs-mock.md) - When to use Fake vs Mock
- [mock-creation.md](references/mock-creation.md) - Extend Mock, no overrides
- [fallback-values.md](references/fallback-values.md) - registerFallbackValue
- [stubbing.md](references/stubbing.md) - Sync, async, thenThrow
- [verification.md](references/verification.md) - verify, verifyNever, called(n)
- [parameters-matchers.md](references/parameters-matchers.md) - Named params, any(), captureAny
- [best-practices.md](references/best-practices.md) - Real/fakes, stub all, toString

## Quick Reference

### Fake vs Mock
- Fake: assert outcomes; Mock: verify interactions

### Stubbing
- Sync: `when(() => mock.method()).thenReturn(value)`
- Async: `thenAnswer((_) async => result)` or `thenReturn(Future.value(result))`

### Fallbacks
- `registerFallbackValue(SomeType())` for every custom type in matchers

### Verification
- `verify(() => mock.method())`, `verifyNever`, `verify(...).called(n)`
