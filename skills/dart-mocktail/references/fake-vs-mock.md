---
title: Fake vs Mock
description: When to use Fake vs Mock
---

# Fake vs Mock

## Fake

- Use when a lightweight, custom subset of behaviour suffices.
- Use when the test asserts on **outcomes** (result values, state).
- Prefer real collaborators or well-tested fakes for outcome-based tests.

## Mock

- Reserve for cases where you must **verify interactions**.
- Use when asserting that specific methods were called, with what args, how many times.
- Extend Mock; stub and verify explicitly.

## Choice

- Outcome assertion → Fake or real collaborator.
- Interaction verification → Mock.
