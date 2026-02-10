---
name: mermaid-diagrams
description: Mermaid diagram syntax for flowcharts, sequence, class, state, module, ER, GitFlow. Use when generating Mermaid diagrams in documentation, technical designs, or architecture.
---

# Mermaid Diagrams

## Overview

Complete Mermaid syntax rules: diagram types, proper formatting, escaping, and when to use each type.

## Reference Files

See detailed documentation for each topic:

- [syntax-rules.md](references/syntax-rules.md) - Declaration, indentation, arrows, close blocks
- [flowcharts.md](references/flowcharts.md) - flowchart TD/LR, nodes, arrows
- [sequence.md](references/sequence.md) - sequenceDiagram, participants, messages
- [class-state.md](references/class-state.md) - classDiagram, stateDiagram-v2
- [module-component.md](references/module-component.md) - Subgraph, component flow
- [data-flow-er-gitflow.md](references/data-flow-er-gitflow.md) - Data flow, erDiagram, gitGraph
- [selection-guide.md](references/selection-guide.md) - When to use each type, Flutter use cases
- [formatting.md](references/formatting.md) - Escaping, pitfalls, validation checklist

## Quick Reference

### Syntax
- `flowchart TD`/`LR` (not deprecated `graph`)
- 2 spaces indent; quotes for special chars; close blocks with `end`

### Flutter Use Cases
- BLoC → stateDiagram-v2; Architecture → flowchart + subgraph; API → sequenceDiagram

### Validation
- Correct type; valid arrows; quoted special chars; blocks closed
