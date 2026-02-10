---
title: Isolates
description: CPU-intensive work off UI thread
---

# Isolates

## When to Use

- Use isolates for CPU-intensive operations.
- Calculations, data processing, heavy JSON parsing.
- Keeps UI thread responsive; avoids frame drops.

## compute()

- Use `compute()` to run work in a separate isolate.
- Simple API: pass function and argument; returns Future with result.
- Function and argument must be top-level or static (isolate can't share object references).

## Use Cases

- JSON.decode for large payloads
- Image processing
- Complex algorithms
- Batch data transformations
