---
title: Patterns
description: Matching, destructuring, nesting, where to use
---

# Patterns

## Concepts

1. Patterns describe shapes of values for matching and destructuring.
2. Matching checks shape, constants, equality, or type.
3. Destructuring extracts and binds parts of matched values.
4. Patterns can nest with outer and inner subpatterns.
5. Use `_` to ignore parts; rest elements for remaining list items.

## Where to Use

6. Variable declarations/assignments, loops, `if-case`/`switch`, collection literals.

## Declarations and Assignments

7. Pattern declarations: `var` or `final` (e.g. `var (a, [b, c]) = ('str', [1, 2]);`).
8. Pattern assignments: `(b, a) = (a, b);`.

## switch/if-case

9. Every `switch` or `if-case` clause contains a pattern; any kind allowed.
10. Case patterns are refutable; failed match continues to next case.
11. Destructured bindings scoped to case body.
12. Logical-or patterns match multiple alternatives in one case.
13. Combine logical-or with guards.
14. Guards run after matching; `false` guards fall through.

## Loops

15. `for (final MapEntry(key: k, value: v) in map.entries)`.

## Object and Record Patterns

16. Object: `var Foo(:one, :two) = foo;` (destructure via getters).
17. Records: destructure positional and named fields directly.

## Benefits

18. Algebraic data types with sealed classes and exhaustive switches.
19. Validation/destructuring of complex data (e.g. JSON) declaratively.
20. Concise alternative to verbose type-checking/destructuring.
