---
title: Code Quality Tools
description: dart format, dart fix, analysis_options, build_runner
---

# Code Quality Tools

## Formatting

Use `dart format` for consistent formatting.

## Fixes

Use `dart fix` to auto-fix errors and conform to analysis options.

## Linting

Use Dart linter with recommended rules. Include `flutter_lints` in analysis_options.yaml:

```yaml
include: package:flutter_lints/flutter.yaml
linter:
  rules:
    # avoid_print: false
    # prefer_single_quotes: true
```

Use HTTPS for URLs in pubspec.yaml (secure_pubspec_urls).

## Code Generation

- Add `build_runner` as dev dependency when using code generation (json_serializable, etc.)
- Run: `dart run build_runner build --delete-conflicting-outputs`
