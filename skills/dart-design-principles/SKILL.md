---
name: dart-design-principles
description: Core software design principles for maintainable Dart/Flutter code. Use when applying SOLID, composition over inheritance, polymorphism over switch/case, immutability, abstraction layers, and code reusability.
---

# Dart Design Principles

## Overview

Design principles for maintainable and scalable code: SOLID, composition, polymorphism over type checking, immutability, and reusability.

## Reference Files

See detailed documentation for each topic:

- [solid.md](references/solid.md) - Single Responsibility, Open/Closed, Liskov, Interface Segregation, Dependency Inversion
- [code-style.md](references/code-style.md) - Concise, declarative, immutability
- [composition-abstraction.md](references/composition-abstraction.md) - Composition over inheritance, interfaces, encapsulation
- [polymorphism.md](references/polymorphism.md) - Polymorphism over switch/case, bad/good example
- [reusability.md](references/reusability.md) - Sharing behavior, utilities, validation, hashCode

## Quick Reference

### SOLID
- Single Responsibility; Open/Closed; Liskov Substitution; Interface Segregation; Dependency Inversion

### Polymorphism
- If all switch cases call same method with same params → use base interface directly
- Avoid type casting when interface provides needed functionality

### Composition
- Prefer composition over inheritance when it adds flexibility
- Use interfaces for contracts; encapsulate internals
