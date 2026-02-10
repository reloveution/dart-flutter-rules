---
title: Composition and Abstraction
description: Composition over inheritance, interfaces, encapsulation
---

# Composition and Abstraction

## Composition Over Inheritance

- Use composition over inheritance for better flexibility and testability.
- Apply when logically justified and provides clear benefits over inheritance.
- Compose behavior from smaller, focused components.

## Abstraction Layers

- Create proper abstraction layers to decouple components.
- Hide implementation details behind abstractions.
- Allow swapping implementations without affecting clients.

## Interfaces

- Use interfaces to define contracts between modules.
- Clients depend on contracts, not concrete types.
- Enables mocking and alternative implementations.

## Encapsulation

- Implement proper encapsulation to hide internal implementation details.
- Expose only what clients need.
- Keep internals private; provide controlled access via methods when needed.
