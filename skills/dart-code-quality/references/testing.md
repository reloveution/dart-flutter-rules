---
title: Testing (Code Quality)
description: run_tests tool, checks, AAA, naming
---

# Testing

## Running

Use `run_tests` tool when available; otherwise `flutter test`.

## Packages

- Unit: `package:test`
- Widget: `package:flutter_test`
- Integration: `package:integration_test`
- Assertions: Prefer `package:checks` over matchers

## Testability

- Dependency injection for testability
- Separate business logic from framework code
- Use matchers for throws (use_test_throws_matchers)

## Best Practices

- Arrange-Act-Assert (Given-When-Then)
- Name tests "should …": `test('counter should start at 0', () { })`
- Wrap in `group()` named after class/feature
- Prefer fakes/stubs over mocks; use mocktail if mocks needed
- Focus on logic that can break; skip trivial assertions
- Each test fails if production regresses

See **flutter-testing** skill for full testing guidance.
