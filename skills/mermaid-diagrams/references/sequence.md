---
title: Sequence Diagrams
description: Participants, messages, blocks
---

# Sequence Diagrams

## Participants

- Define with `participant Name as Label`

## Message Types

- `->>` solid arrow (async)
- `->` sync
- `-->>` dotted arrow (response)

## Blocks

- `loop`, `alt`, `opt`, `par` — always close with `end`

## Example

```mermaid
sequenceDiagram
    participant A as Client
    participant B as Server
    A->>B: Request
    Note right of B: Processing
    B-->>A: Response
    loop Retry Logic
        B->>B: Validate
    end
```
