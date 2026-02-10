---
title: Image Optimization
description: Caching, Image.asset
---

# Image Optimization

## Caching

- Use `Image.asset` with proper caching instead of loading images repeatedly.
- Asset images are cached automatically.
- For network images, use `cached_network_image` or similar.

## Avoid Repeated Loading

- Don't reload same image in a loop or on every rebuild.
- Caching and proper image provider configuration prevent redundant I/O.
