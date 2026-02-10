---
title: Code Reusability & Organization
description: Sharing behavior, utilities, validation, hashCode
---

# Code Reusability & Organization

## Sharing Behavior

- Use inheritance and/or composition to share behavior without duplication.
- Choose based on "is-a" vs "has-a" relationship and flexibility needs.

## Utility Functions

- Create utility functions for repeated logic patterns.
- Extract common operations into reusable helpers.
- Prefer extension methods for type-specific utilities.

## Validation

- Implement proper data validation using validators.
- Centralize validation logic; reuse across boundaries.
- Validate at boundaries (input, API response).

## Equality and HashCode

- Implement proper `hashCode` and `operator==` for custom classes.
- Override both together; use for collections, maps, identity.
- Consider freezed or Equatable for generated implementations.
