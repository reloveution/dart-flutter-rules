---
title: Try-Catch and Exception vs Error
description: When to use, specific catch, Error vs Exception, rethrow
---

# Try-Catch and Exception vs Error

## When to Use Try-Catch

- Use try-catch only for external API calls and system operations.
- At boundaries: HTTP, database, file I/O, platform channels.
- Don't wrap pure business logic that uses Result<T>.

## Specific Catch

- Use specific catch clauses: `on SpecificException catch (e) {}`.
- Avoid generic `catch (e)` when you can narrow the type.
- Handle expected failure modes explicitly.

## Error vs Exception

- **Exception**: Expected failures (network, validation, I/O). Catch these.
- **Error**: Programming errors (AssertionError, StateError). Never catch.
- Only throw Error and subclasses for programming errors.
- Never catch Error—let it propagate for debugging.

## Rethrow

- Use `rethrow` instead of `throw e` to preserve stack trace.
- Use when catching to log or convert, then propagating.

## Finally

- Avoid control flow in finally blocks.
- Use try-catch properly; finally for cleanup only.
- Don't return or throw from finally for control flow.
