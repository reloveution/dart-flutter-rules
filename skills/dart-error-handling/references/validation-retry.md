---
title: Validation and Retry
description: Input validation, network retry
---

# Validation and Retry

## Input Validation

- Validate user input and provide immediate feedback.
- Fail fast at boundaries; don't propagate invalid data.
- Return Result.failure with clear validation messages.

## Network Retry

- Handle network errors gracefully with retry mechanisms.
- Exponential backoff for transient failures.
- Distinguish retriable vs non-retriable errors.
- Set max retries; fail with Result after exhaustion.
