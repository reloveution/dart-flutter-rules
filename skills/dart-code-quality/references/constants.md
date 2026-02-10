---
title: Constants and Imports
description: Magic numbers, library organization
---

# Constants and Imports

## Constants

- No magic numbers; use AppConstants
- Descriptive names for persistent resources: `_todoTableName` not `_kTableTodo`

## Imports

- Relative imports for same directory structure
- Package imports when necessary
- Consistent combinator order (show, hide)
- Library annotations when creating libraries
- No dangling doc comments
- No private types in public API
- No imports from package `src`
- Package paths inside `lib/`; no `/lib/` or `../` segments
