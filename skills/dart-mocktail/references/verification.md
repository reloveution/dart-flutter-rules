---
title: Verification
description: verify, verifyNever, called(n)
---

# Verification

## verify

- `verify(() => mock.method())` — method was called.
- Use for interaction assertions.

## verifyNever

- `verifyNever(() => mock.method())` — method was not called.

## called(n)

- `verify(() => mock.method()).called(n)` — assert call count.
- Use when exact number of invocations matters.

## Named Parameters

- Supply all named parameters in verify.
- Use `any(named: 'param')` when the exact value is irrelevant.
