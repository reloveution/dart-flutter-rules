---
title: Datasource Naming Patterns
description: Package prefix, interface format, folders
---

# Datasource Naming Patterns

## Interface Format

- `I{FeatureMarking}Dts` (e.g. `IDocumentDts`, `IApiMagDecDts`).

## Implementation with Package

- For implementations using external packages, include package name or abbreviation as prefix.
- Format: `{PackageName}{FeatureMarking}DtsImpl`.
- Examples: `ExcelExportDtsImpl`, `NoaaApiMagDecDtsImpl`.

## Multiple Datasources per Feature

- When a repository handles multiple datasources, create separate folders per direction.
- Under implementation folder: `api/`, `excell/`, `csv/` etc.
- Keeps datasource types organized by source/direction.
