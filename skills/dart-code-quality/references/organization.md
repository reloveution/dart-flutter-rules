---
title: Code Organization
description: Nesting, DRY, class member order
---

# Code Organization

## Nesting

Extract methods when nesting exceeds 3 levels.

## DRY

- Meaningful variable names
- No duplication; extract common functionality
- No self-assignments (`x = x`)
- Use declared variables; no wildcards

## Avoid

- Unnecessary overrides
- Unnecessary parentheses
- Raw strings when regular work
- Parameter assignments
- Returning null from void functions
- Returning `this` (except builder pattern)
- Setters without getters

## Class Member Order

1. Static constants (static const)
2. Class fields (final → regular)
3. Constructor
4. Getters/Setters
5. Lifecycle (initState, dispose)
6. Override methods
7. Public methods
8. Private methods

Helpers/internal methods after external methods. Group related methods. Single responsibility.
