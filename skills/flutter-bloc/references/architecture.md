---
title: Bloc Architecture
description: Layer separation, repository injection, bloc coordination
---

# Bloc Architecture

## Layers

1. Separate features into: Presentation, Business Logic, Data.
2. **Data Layer**: Retrieves and manipulates data (databases, network).
3. Structure Data Layer: repositories (wrappers) + data providers (CRUD).
4. **Business Logic**: Responds to presentation input, communicates with repositories, builds states.
5. **Presentation**: Renders UI from bloc states, handles user input and lifecycle.

## Dependency Injection

6. Inject repositories into blocs via constructors.
7. Blocs must not directly access data providers.

## Bloc-to-Bloc

8. Avoid direct bloc-to-bloc communication (tight coupling).
9. To coordinate: use BlocListener in presentation to listen to one bloc and add events to another.

## Shared Data

10. Inject the same repository into multiple blocs.
11. Let each bloc listen to repository streams independently.

## Principles

12. Loose coupling between layers and components.
13. Structure project consistently and intentionally.
