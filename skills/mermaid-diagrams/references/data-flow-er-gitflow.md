---
title: Data Flow, ER, GitFlow
description: Data flow, erDiagram, gitGraph
---

# Data Flow

- `flowchart LR` for horizontal flow
- Rectangles for transformation steps
- `-->` for data movement
- Include external systems, databases

# Entity Relationship

- `erDiagram`
- Relationships: `||--o{` one-to-many, `||--||` one-to-one, `}o--o{` many-to-many
- Attributes in curly braces
- PK for primary keys, FK for foreign keys, UK for unique

# GitFlow

- `gitGraph`
- `branch branchName`, `checkout branchName`, `merge branchName`
- `commit id: "label"` for commit nodes
