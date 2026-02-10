---
title: Data Transfer & Serialization
description: DTOs, JSON, copyWith, validation
---

# Data Transfer & Serialization

## DTOs

- Use DTOs for data transfer between layers.
- Keep DTOs separate from domain entities.

## JSON

- Implement proper serialization: `fromJson` / `toJson`.
- Handle nullability and type conversions explicitly.
- Use code generation (json_serializable, freezed) when appropriate.

## Immutable Data Classes

- Use data classes with `copyWith` methods for immutable data.
- Enable easy updates without mutating original.

## Validation

- Implement proper data validation at boundaries.
- Validate on input (API response, user input) before use.
- Fail fast with clear error messages.
