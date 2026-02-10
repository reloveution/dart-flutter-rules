---
title: Branches
description: if, if-case, switch statements and expressions, guards
---

# Branches

## if

1. Use `if` for conditional branching; conditions must evaluate to `bool`.
2. Optional `else` and `else if` for multi-branch logic.

## if-case

3. Use `if-case` to match and destructure against a single pattern: `if (pair case [int x, int y]) { ... }`.
4. When pattern matches, bound variables are in scope for that branch.
5. If pattern does not match, control continues to `else` if it exists.

## switch Statement

6. Use `switch` to match a value against multiple patterns.
7. Matching `case` executes body and exits; no explicit `break` needed.
8. Non-empty cases may end with `continue`, `throw`, or `return`.
9. Use `default` or `_` for unmatched values.
10. Empty `case` falls through; use `break` to stop fallthrough.
11. Use labeled `continue` for non-sequential fallthrough.
12. Logical-or: `case a || b` to share body between cases.

## switch Expression

13. Use `switch` expressions for expression-based branching; use `=>`, separate branches with commas.
14. Default branch uses `_`.

## Exhaustiveness

15. Dart enforces exhaustiveness at compile time.
16. Ensure exhaustiveness via `_`/`default`, enum switching, or sealed types.
17. Mark classes `sealed` for exhaustiveness checks on subtypes.

## Guards

18. Add `when` to constrain: `case pattern when condition:`.
19. Guards evaluated after pattern matching.
20. If guard is `false`, execution proceeds to next case.
