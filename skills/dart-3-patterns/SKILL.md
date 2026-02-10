---
name: dart-3-patterns
description: Dart 3 patterns including switch/if-case, pattern matching, sealed classes, and records. Use when writing exhaustive switches, destructuring, pattern matching on types, or returning multiple values with records.
---

# Dart 3 Patterns

## Overview

Dart 3 control-flow and pattern-matching reference: conditional branches, switch exhaustiveness, pattern destructuring, pattern operators, and records.

## Reference Files

See detailed documentation for each topic:

- [branches.md](references/branches.md) - if, if-case, switch statement/expression, guards, exhaustiveness
- [patterns.md](references/patterns.md) - Matching, destructuring, nesting, where to use
- [pattern-types.md](references/pattern-types.md) - Logical-or, relational, cast, null-check, list, map, record, object
- [records.md](references/records.md) - Record syntax, access, equality, when to use

## Quick Reference

### Switch
- No `break` needed; case body runs and exits
- `default` or `_` for unmatched
- Switch expressions: `=>` branches, `_` for default
- Guards: `case X when condition:`

### if-case
- Single pattern match with destructuring: `if (pair case [int x, int y]) { }`
- Variables in scope when matched
- `else` when pattern doesn't match

### Patterns
- Logical-or: `case a || b`
- Object: `var Foo(:one, :two) = foo;`
- Records: `(a, b: named)`
- List/map: match by shape

### Sealed Classes
- Mark `sealed` for exhaustiveness checks
- All subtypes must be handled in switch

### Records
- Immutable: `(a, b: name)`
- Return multiple values; destructure with patterns
- Type: `(int, String, {bool flag})`
