---
title: Error Handling (Code Quality)
description: UI errors, catch clauses, rethrow
---

# Error Handling

## UI

Handle errors gracefully. Show user-friendly messages; never expose technical details.

## Catch Clauses

Use specific catch: `on SpecificException catch (e)` instead of generic `catch (e)`.

## Exception vs Error

- Never catch `Error` or subclasses (AssertionError)
- Only catch `Exception`
- Use `rethrow` not `throw e` to preserve stack trace

## Finally

Avoid control flow in finally blocks.
