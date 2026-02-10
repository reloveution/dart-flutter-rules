---
title: General Syntax Rules
description: Declaration, indentation, arrows, closing blocks
---

# General Syntax Rules

## Declaration

- Always start with diagram type declaration on first line.
- Use correct directive: flowchart, sequenceDiagram, classDiagram, etc.

## Indentation

- Use 2 spaces for nested elements and subgraphs.

## Special Characters

- Escape special characters: wrap text in quotes.
- `A["Text with → arrow"]`

## Arrows

- Validate arrow syntax; use appropriate types per diagram.
- Flowchart: `-->`, `-.->`, `==>`
- Sequence: `->>`, `-->>`

## Blocks

- Close all blocks with proper endings: `end`
- Applies to: subgraph, loop, alt, opt, par
