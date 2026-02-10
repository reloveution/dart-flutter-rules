---
title: Pattern Types
description: Logical-or, logical-and, relational, cast, null-check, list, map, record, object
---

# Pattern Types

## Precedence

1. Parentheses control evaluation order.

## Logical

2. **Logical-or** (`p1 || p2`): Matches if any branch matches; left-to-right; same variables in each branch.
3. **Logical-and** (`p1 && p2`): Both subpatterns must match; variable names must not overlap.

## Relational and Cast

4. **Relational** (`==`, `!=`, `<`, `>`, `<=`, `>=`): Compare against constants; combine with logical-and for ranges.
5. **Cast** (`subpattern as Type`): Assert before matching; throws on mismatched type.

## Null

6. **Null-check** (`subpattern?`): Match non-null; bind as non-nullable.
7. **Null-assert** (`subpattern!`): Require non-null; throw otherwise.

## Constant and Variable

8. **Constant**: Match equality to constants (const constructors, collections).
9. **Variable** (`var name`, `final Type name`): Bind new variables.
10. **Identifier**: Variable or constant depending on context; `_` is wildcard.
11. **Parenthesized**: Control precedence.

## Collection Patterns

12. **List**: Match by position; lengths align unless using rest elements.
13. **Rest** (`...`, `...rest`): Arbitrary-length or capture remaining.
14. **Map**: Match by key; missing keys throw `StateError`.

## Record and Object

15. **Record**: Match by shape; destructure positional and named.
16. **Object**: Match type and destructure via getters; extra fields ignored.
17. **Wildcard** (`_`, `Type _`): Match without binding.

## Nesting

18. All types nest and combine for expressive matching.
