---
name: flutter-widget-patterns
description: Flutter widget patterns. Use when building UI, fixing layout errors, theming, composing widgets, GoRouter, accessibility, or assets.
---

# Flutter Widget Patterns

## Overview

Build optimization, composition, layout, theming, navigation, accessibility.

## Reference Files

- [core-patterns.md](references/core-patterns.md) - Composition, build optimization, Container alternatives, context
- [layout.md](references/layout.md) - Overflow, Row/Column, lists, Stack, OverlayPortal
- [gorouter-navigation.md](references/gorouter-navigation.md) - GoRouter, Navigator
- [theming-visual.md](references/theming-visual.md) - ThemeData, ThemeExtension, fonts, visual design
- [performance.md](references/performance.md) - ListView.builder, compute(), RepaintBoundary
- [accessibility-assets.md](references/accessibility-assets.md) - A11Y, images

## Quick Reference

- **Composition:** Separate widgets; no widget-returning methods; pass callbacks not state managers
- **Container:** Use SizedBox, ColoredBox, DecoratedBox instead
- **Context:** Check mounted before dialogs; get controllers from context in tree
- **Layout:** Expanded/Flexible for Row/Column; ListView.builder for long lists
- **Theme:** ThemeData, ColorScheme.fromSeed, ThemeExtension; 8-digit hex colors
- **Navigation:** GoRouter for main; Navigator for dialogs
