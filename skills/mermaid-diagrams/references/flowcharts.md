---
title: Flowcharts
description: flowchart TD/LR, nodes, arrows
---

# Flowcharts (Modern)

## Directive

- Use `flowchart TD` (top-down) or `flowchart LR` (left-right).
- Do NOT use deprecated `graph`.

## Node Shapes

- `[rectangle]`, `(rounded)`, `{diamond}`, `((circle))`, `([stadium])`

## Arrows

- `-->` solid
- `-.->` dotted
- `==>` thick
- Labels: `-->|Yes|` or `-->|No|`

## Example

```mermaid
flowchart TD
    A[Start] --> B{Decision}
    B -->|Yes| C[Action 1]
    B -->|No| D[Action 2]
    C --> E([End])
    D --> E
```
