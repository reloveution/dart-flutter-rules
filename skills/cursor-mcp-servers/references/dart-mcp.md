---
title: Dart MCP Server
description: Development tools for Dart/Flutter projects
---

# Dart MCP Server

## When to Use

- Dart/Flutter code analysis, formatting, tests
- pub.dev package search
- Dart Tooling Daemon (widget tree, hot reload)
- Creating projects

## When NOT to Use

- Web search (use Firecrawl or web_search)

## Essential: add_roots First

- `mcp_dart_add_roots` must be called before workspace-dependent commands.
- Format: `[{uri: "file:///absolute/path", name: "optional"}]`.

## Commands by Category

**Project:** create_project, add_roots, remove_roots, pub (add/get/remove/upgrade), pub_dev_search

**Analysis:** analyze_files, dart_fix, dart_format

**Symbols:** resolve_workspace_symbol, hover, signature_help

**DTD (running app):** connect_dart_tooling_daemon (needs URI from user), hot_reload, get_runtime_errors, get_widget_tree, get_selected_widget

**Tests:** run_tests (roots required; testRunnerArgs: name, tags, platform, timeout, fail-fast, coverage)

## Priority

High for all Dart/Flutter development tasks.
