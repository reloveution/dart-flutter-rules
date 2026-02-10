---
title: Logging and Reporting
description: Structured logging, production reporting, platform-specific
---

# Logging and Reporting

## Structured Logging

- Use structured logging with context information.
- Include: error type, message, stack trace, relevant IDs.
- Use `log()` from dart:developer, not print.

## Production Reporting

- Implement proper error reporting for production apps.
- Integrate with crash reporting (e.g. Firebase Crashlytics).
- Avoid exposing sensitive data in reports.

## Platform-Specific

- Handle platform-specific errors appropriately.
- Map platform exceptions to domain Result failures.
- Provide platform-appropriate user messages when needed.
