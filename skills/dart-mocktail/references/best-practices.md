---
title: Best Practices
description: Real/fakes, stub all, toString
---

# Best Practices

## Prefer Real/Fakes

- Prefer real collaborators or well-tested fakes when the test asserts on outcomes.
- Use mocks only when you need to verify interaction patterns.
- Outcome-based tests are often more robust than interaction-based.

## Stub Every Method

- Stub every dependency method expected to execute during the test.
- Prevents MissingStub errors at runtime.
- Plan which code paths the test exercises and stub accordingly.

## toString and Equality

- Understand the string representation of types you match.
- Ensures equals and toString-based assertions behave deterministically.
- Custom types used in matchers should have consistent `==` and `toString`.
