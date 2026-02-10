---
title: Result Pattern
description: Result<T>, convert to failures, UI feedback
---

# Result<T> Pattern

## Use Everywhere

- Use Result<T> for all business operations, including synchronous ones.
- Replace throwing exceptions in business logic.
- Convert caught exceptions to Result<T> failures immediately.

## Conversion

- Catch at boundary (API, database, file I/O).
- Convert to `Result.failure(error)` or `Result<T>.failure(error)`.
- Never let exceptions escape business logic layer.

## UI Feedback

- Result<T> can be used as message wrapper for UI feedback.
- Snackbars, dialogs, inline messages.
- `failure.message` or `failure.toUserMessage()` for display.
