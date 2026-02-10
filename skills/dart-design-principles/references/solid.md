---
title: SOLID Principles
description: Single Responsibility, Open/Closed, Liskov, Interface Segregation, Dependency Inversion
---

# SOLID Principles

## Single Responsibility

- Each class should have only one reason to change.
- Split classes that handle multiple concerns.
- One responsibility per class.

## Open/Closed

- Classes open for extension, closed for modification.
- Use interfaces and inheritance.
- Add behavior via new implementations, not by editing existing code.

## Liskov Substitution

- Subtypes must be substitutable for their base types.
- Maintain behavioral contracts.
- A subtype should not break expectations of code using the base type.

## Interface Segregation

- Create specific interfaces rather than large, general-purpose ones.
- Clients shouldn't depend on unused methods.
- Split fat interfaces into focused ones.

## Dependency Inversion

- Depend on abstractions, not concretions.
- High-level modules shouldn't depend on low-level modules.
- Both depend on abstractions (interfaces).
