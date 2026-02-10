---
title: Layout Best Practices
description: Overflow, Row/Column, lists, Stack, OverlayPortal
---

# Common Layout Errors

- **RenderFlex overflowed:** Row/Column with unbounded children — wrap in Flexible or Expanded, or add constraints
- **Vertical viewport unbounded height:** ListView/Scrollable inside Column — wrap in Expanded, SizedBox, or SliverFillRemaining
- **InputDecorator unbounded width:** TextField/InputDecorator — wrap in Expanded, SizedBox, or parent with fixed width
- **setState during build:** Don't call setState/showDialog in build; use callbacks or addPostFrameCallback sparingly
- **ScrollController multiple:** One ScrollController per scroll view; detach before reuse
- **RenderBox not laid out:** Unconstrained widgets (often ListView/Column) — add size or wrap in constraint-passing widgets
- Use Flutter Inspector for constraint chain analysis

# Row and Column

- **Expanded:** Child fills remaining space along main axis
- **Flexible:** Child shrinks to fit, may not grow; don't combine Flexible and Expanded in same Row/Column
- **Wrap:** Widgets that overflow Row/Column move to next line

# General Content

- **SingleChildScrollView:** Content larger than viewport, fixed size
- **ListView/GridView:** Always use builder constructor for long lists
- **FittedBox:** Scale or fit child within parent
- **LayoutBuilder:** Responsive layouts based on available space

# Stack

- **Positioned:** Precise placement by anchoring to edges
- **Align:** Position using Alignment.center etc.

# OverlayPortal

- Use for dropdowns, tooltips "on top" of everything
- Manages OverlayEntry for you
