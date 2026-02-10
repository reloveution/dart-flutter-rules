---
title: Text Escaping and Validation
description: Quotes, HTML entities, pitfalls, checklist
---

# Text Escaping

- Wrap text with special symbols in quotes: `A["Text with → arrow"]`
- HTML entities: `#8594;` for →, `#9824;` for ♠
- Line breaks: `<br>` — `A["Line 1<br>Line 2"]`

# Common Pitfalls

**Bad:** `graph TD`, unescaped `→`, deprecated `graph`

**Good:** `flowchart TD`, quotes around text, `#8594;` for arrows

# Validation Checklist

Before finalizing:
- Correct diagram type declaration
- All arrows use proper syntax
- Special characters escaped with quotes
- Blocks (subgraph, loop, alt) properly closed
- Node shapes match intent
- Text labels clear and formatted
