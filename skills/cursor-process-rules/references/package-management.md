---
title: Package Management
description: Pub tool, add, remove, dev deps
---

# Package Management

## Preferred Tool

- Use the `pub` tool (or MCP `mcp_dart_pub`) when available.
- Prefer over raw `flutter pub add` commands.

## Adding Dependencies

- **Regular:** `pub add <package>` or `flutter pub add <package_name>`
- **Dev:** `pub add dev:<package>` or `flutter pub add dev:<package_name>`
- **Override:** `override:<package>:1.0.0` for dependency overrides

## Removing

- `dart pub remove <package_name>`

## Discovery

- Use `pub_dev_search` (or MCP) to find packages when needed.
- Identify most suitable and stable package from pub.dev.
