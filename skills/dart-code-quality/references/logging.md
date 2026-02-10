---
title: Logging and Debugging
description: Structured logging, print vs log, toString, assert
---

# Logging and Debugging

## Do Not Use

- No `print` or `debugPrint` in production
- No trailing comments
- No new comments; only TODO in English allowed
- Do not modify existing comments
- Do not remove `log()` when cleaning print/debugPrint

## Structured Logging

Use `log` from `dart:developer` for structured logging (integrates with Dart DevTools):

```dart
import 'dart:developer' as developer;

developer.log('User logged in successfully.');

try {
  // ... code that might fail
} catch (e, s) {
  developer.log(
    'Failed to fetch data',
    name: 'myapp.network',
    level: 1000, // SEVERE
    error: e,
    stackTrace: s,
  );
}
```

Use `logging` package for log levels (debug, info, warning, error).

## Comments

- Verify comment references (check_comment_references)
- Specify language in doc code blocks
- TODO format: `TODO(username):` when using TODO

## Linter Ignores

Document reasons when ignoring linter rules.

## Debugging

- Implement `toString()` for debugging
- Use `assert` for development-time checks; always provide messages
