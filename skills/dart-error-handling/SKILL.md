---
name: dart-error-handling
description: Error handling patterns for Dart/Flutter. Use when implementing Result<T>, exception vs Error, try-catch at boundaries, validation, retry, logging, and resource cleanup.
---

# Dart Error Handling

## Overview

Error handling with Result<T>, specific exceptions, try-catch at boundaries, validation, retry, logging, and resource cleanup.

## Reference Files

See detailed documentation for each topic:

- [prevention.md](references/prevention.md) - Anticipate errors, specific types, meaningful messages
- [result.md](references/result.md) - Result<T>, convert to failures, UI feedback
- [try-catch.md](references/try-catch.md) - When to use, specific catch, Error vs Exception, rethrow
- [validation-retry.md](references/validation-retry.md) - Input validation, network retry
- [logging-reporting.md](references/logging-reporting.md) - Structured logging, production, platform
- [resources.md](references/resources.md) - Close sinks, avoid leaks

## Quick Reference

### Result<T>
- All business logic returns Result; no throwing
- Convert caught exceptions to Result.failure at boundaries

### Exception vs Error
- Catch Exception; never catch Error
- Use `rethrow` to preserve stack trace

### Try-Catch
- Only for external API, database, system operations
- Specific catch: `on SpecificException catch (e)`

### Resources
- Close StreamController, IOSink; avoid leaks
