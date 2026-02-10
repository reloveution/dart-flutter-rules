---
title: Theming and Visual Design
description: ThemeData, fonts, Material 3, accessibility
---

# ThemeData and Material 3

- Centralized ThemeData for consistent app-wide style
- ColorScheme.fromSeed() for light/dark palettes
- Define theme and darkTheme for MaterialApp
- themeMode for toggle (ThemeMode.light, dark, system)

# ThemeExtension

- For custom tokens not in ThemeData
- Extend ThemeExtension<T>; implement copyWith and lerp
- Register in ThemeData.extensions
- Access via Theme.of(context).extension<MyColors>()!

# Fonts

- google_fonts package; one or two font families
- Typographic scale: displayLarge, titleLarge, bodyMedium, labelSmall etc.
- Line height 1.4x–1.6x; line length 45–75 chars

# WidgetStateProperty

- resolveWith for state-dependent values (e.g. pressed color)
- WidgetStateProperty.all when same for all states

# Visual Design

- Theme.of(context).textTheme
- Responsive: MediaQuery, LayoutBuilder
- Implement loading and error states
- RepaintBoundary for expensive painters
- AnimatedBuilder for complex animations
- GestureDetector, focus management, form validation, keyboard handling
- Cancel subscriptions when leaving widgets

# Avoid

- Web libraries in Flutter — use Flutter-specific alternatives
