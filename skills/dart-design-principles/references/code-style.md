---
title: Code Style Principles
description: Concise, declarative, immutability
---

# Code Style Principles

## Concise and Declarative

- Write concise, modern, technical Dart code.
- Prefer functional and declarative patterns.
- Avoid verbose imperative style when a clear expression suffices.

## Immutability

- Prefer immutable data structures.
- Widgets (especially `StatelessWidget`) should be immutable.
- Use `final` fields; `copyWith` for updates; avoid mutable state where possible.
