---
name: dart-code-quality
description: Core code quality rules for clean, maintainable Dart/Flutter code. Use when formatting code, writing documentation, handling async/null safety, organizing classes, or following Dart best practices.
---

# Dart Code Quality

## Overview

Core rules for clean, maintainable Dart and Flutter code. Covers logging, async, null safety, documentation, style, and best practices.

## Reference Files

See detailed documentation for each topic:

- [logging.md](references/logging.md) - Structured logging, print vs log, toString, assert
- [tools.md](references/tools.md) - dart format, dart fix, analysis_options, build_runner
- [async.md](references/async.md) - Future, Stream, unawaited, pass-through
- [null-safety.md](references/null-safety.md) - Avoid !, extract nullable, null-aware operators
- [functions.md](references/functions.md) - Arrow functions, parameters, BlocBuilder style
- [documentation.md](references/documentation.md) - Doc comments, API design
- [style.md](references/style.md) - Naming, line length, strings, formatting
- [control-flow.md](references/control-flow.md) - Guard clauses, early returns
- [types.md](references/types.md) - Avoid dynamic, sealed, explicit types
- [constructors.md](references/constructors.md) - Initializing formals, super params
- [variables.md](references/variables.md) - final, ternary over if-else
- [collections.md](references/collections.md) - Literals, functional methods, equality
- [organization.md](references/organization.md) - Nesting, DRY, class member order
- [error-handling.md](references/error-handling.md) - UI errors, catch, rethrow
- [constants.md](references/constants.md) - Magic numbers, imports
- [performance.md](references/performance.md) - Build methods, const
- [testing.md](references/testing.md) - run_tests, checks, AAA, naming
- [utilities.md](references/utilities.md) - Getters, enum byName, validation

## Quick Reference

### Logging
Use `developer.log()` from `dart:developer`; never print in production.

### Async
`Future<T> m() => other();` for pass-through; `unawaited()` for fire-and-forget.

### Null Safety
Extract nullable to local; avoid `!`; use `??`, `?.`.

### Formatting
80 chars, trailing commas, `dart format`, `dart fix`.

### Class Order
static const → fields → constructor → getters → lifecycle → overrides → public → private

## Related Skills

- **dart-error-handling** – Result type, business logic exceptions
- **flutter-testing** – Full testing guide
