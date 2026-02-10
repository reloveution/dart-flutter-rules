---
title: Stubbing
description: Sync, async, thenThrow
---

# Stubbing

## Synchronous

- `when(() => mock.method()).thenReturn(value)` for fixed return.
- `thenAnswer((invocation) => value)` for dynamic response.
- `thenThrow(error)` for failure branches.

## Asynchronous

- Always return Future values.
- `thenAnswer((_) async => result)` — preferred for async.
- `thenReturn(Future.value(result))` — alternative.
- Keeps method signature consistent.

## Stub Every Method

- Stub every dependency method the test expects to execute.
- Avoids MissingStub errors at runtime.
- Unstubbed calls cause test failure.
