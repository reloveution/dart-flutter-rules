---
title: Error Prevention
description: Anticipate errors, specific types, meaningful messages
---

# Error Prevention

## Anticipate

- Anticipate and handle potential errors.
- Don't let your code fail silently.
- Design for failure paths explicitly.

## Specific Error Types

- Implement specific error types instead of generic Exception.
- Enables targeted handling and clearer stack traces.
- Example: `NetworkFailure`, `ValidationError`, `NotFoundError`.

## Meaningful Messages

- Provide meaningful error messages with actionable guidance.
- Help users and developers understand what went wrong.
- Include context (e.g. which field failed, suggested next step).
