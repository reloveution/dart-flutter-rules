---
title: Code Styling and Formatting
description: Line length, naming, strings, trailing commas
---

# Code Styling and Formatting

## Naming

- **Classes**: PascalCase
- **Members, variables, functions, enums**: camelCase
- **Files**: snake_case

## Line Length

80 characters or fewer.

## Strings

- Extract user-facing strings to localization; no hardcoding
- Single quotes (prefer_single_quotes)
- Interpolation over `+`: `$variable`
- Adjacent concatenation: `'a' 'b'` over `'a' + 'b'`
- Alt quotes to avoid escapes: `"text 'with' quotes"`
- No unnecessary escapes or interpolations

## Formatting

- Trailing commas in multi-line lists, calls
- Newline at end of file
- Leading newlines in multiline strings
- Consistent import combinators (show, hide)
- Avoid unnecessary `new`, `const`, constructor names

## Conciseness

Write as short as possible while staying clear.
