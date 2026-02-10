---
title: Workflow Examples
description: Key usage patterns
---

# Workflow Examples

## Package Info (flutter_bloc)

`mcp_dart_pub_dev_search(query: "flutter_bloc")`

## Add Dependency

`mcp_dart_pub(command: "add", packageName: "bloc", roots: [{root: "file:///path"}])`

## Analyze Project

1. add_roots
2. analyze_files
3. dart_fix, dart_format

## Web Content (Dart docs)

1. web_search for URLs, or firecrawl_map
2. firecrawl_scrape(url, formats: ["markdown"], onlyMainContent: true)

## Batch Scrape

1. batch_scrape(urls, options)
2. check_batch_status(id)

## ML Models

model_search with author, task, library filters → hub_repo_details for specifics

## DTD (Running App)

connect_dart_tooling_daemon(uri from user) → get_widget_tree, hot_reload
