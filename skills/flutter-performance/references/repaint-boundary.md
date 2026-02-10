---
title: RepaintBoundary
description: Complex custom painters
---

# RepaintBoundary

## When to Use

- Use `RepaintBoundary` for complex custom painters.
- Isolates repaint region; changes inside don't force repaint of siblings/parent.
- Use when a subtree has expensive painting and updates independently.

## Trade-off

- Adds a layer; use when the repaint cost saved outweighs layer cost.
- Profile before and after to validate benefit.
