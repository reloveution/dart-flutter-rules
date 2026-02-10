---
title: Records
description: Record syntax, access, equality, when to use
---

# Records

## Basics

1. Immutable aggregates bundling multiple values.
2. Fixed-sized, heterogeneous, strongly typed.
3. First-class: store, nest, pass, collect.

## Syntax

4. Expressions: `('first', a: 2)` with positional and/or named fields.
5. Type annotations mirror expression syntax.
6. Named field names are part of the type (shape).
7. Positional labels in type annotations are documentary only.

## Access

8. Positional: `$1`, `$2`, etc.
9. Named: via identifiers.
10. Records are immutable; no setters.

## Equality

11. Structural typing—shape defines type.
12. Equal when shapes and values match; named field order irrelevant.
13. `hashCode` and `==` auto-generated from structure and values.

## Destructuring

14. Destructure with patterns: `final (:name, :age) = userInfo(json);`.

## When to Use

15. Return multiple values; leaner than classes/lists/maps for simple tuples.
16. Lists of records for uniform tuples.
17. Use `typedef` aliases for readability.
18. Updating typedef doesn't guarantee compatibility; classes provide encapsulation.
19. Extension types can wrap records.
20. Prefer records for simple immutable grouping; choose classes when abstraction or behavior is needed.
