---
name: dart-naming-conventions
description: Project naming conventions for Dart/Flutter. Use when naming interfaces (I prefix), implementations (Impl), use cases (Ucs), datasources (Dts), extensions (X), mixins (Mxn), or organizing feature/datasource folders.
---

# Dart Naming Conventions

## Overview

Project-specific naming: interfaces, implementations, use cases, datasources, extensions, mixins, files, and abbreviations.

## Reference Files

See detailed documentation for each topic:

- [autocomplete.md](references/autocomplete.md) - $ prefix for rare functions
- [interfaces-impl.md](references/interfaces-impl.md) - I prefix, Impl suffix
- [extensions-mixins.md](references/extensions-mixins.md) - X suffix, Mxn suffix
- [use-cases-datasources.md](references/use-cases-datasources.md) - Ucs, Dts, repo, dts
- [datasource-patterns.md](references/datasource-patterns.md) - Package prefix, I{Feature}Dts, folders
- [variables-abbreviations.md](references/variables-abbreviations.md) - Clear context
- [general-naming.md](references/general-naming.md) - snake_case, PascalCase, camelCase, acronyms

## Quick Reference

| Type | Convention | Example |
|------|------------|---------|
| Interface | I prefix | IExportRepo |
| Implementation | Impl suffix | MagDecRepoImpl |
| Use case | Ucs suffix | GetMagDecUcs |
| Datasource | Dts suffix | IApiMagDecDts |
| Extension | X suffix | ExtExcelPrjBaseSheet |
| Mixin | Mxn suffix | MxnExcelFormatting |
| Rare function | $ prefix | $helper |
| File | snake_case | user_service.dart |
| Class | PascalCase | UserService |
| Acronym 3+ chars | Capitalize as word | HttpClient |
