---
title: Functions and Callbacks
description: Arrow functions, parameters, BlocBuilder style
---

# Functions and Callbacks

## Arrow Functions

Prefer arrow functions for single-expression functions and callbacks.

For widget build methods and BlocBuilder callbacks: prefer arrow functions with ternary over if-else. Use `_` for unused parameters.

## Parameters

- Named parameters for functions with more than 2 parameters
- Required named parameters before optional ones
- Avoid positional boolean parameters
- Avoid redundant argument values (e.g. `true` for bool params)
- Parameters are final; no assignments

## Utilities

- Extension methods over static methods for utilities
- Avoid static methods for business logic

## Typedefs

Use typedef for complex signatures. Prefer generic syntax: `typedef F<T> = R Function(T);`

## Style

- Prefer `void f() {}` over `void Function() v = () {}`
- Use tear-offs: `list.forEach(print)` not `list.forEach((x) => print(x))`
- Functions: short, single purpose, under 20 lines
