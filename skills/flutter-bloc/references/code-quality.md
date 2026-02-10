---
title: Code Quality and Linting
description: bloc_lint, bloc_tools, analysis_options
---

# Code Quality and Linting

## bloc_lint

1. Use bloc_lint to enforce Bloc best practices.
2. Configure in analysis_options.yaml with recommended rules.
3. Available rules: avoid_flutter_imports, avoid_public_fields, avoid_public_bloc_methods, prefer_bloc, prefer_cubit, prefer_void_public_cubit_methods.

## bloc_tools

4. Use bloc_tools CLI for scaffolding and workflow.
5. Install globally: `dart pub global activate bloc_tools`.
6. Run lint: `bloc lint` (from bloc_tools).

## Rules

7. Avoid Flutter imports in blocs, cubits, repositories.
8. Do not expose public fields on Bloc/Cubit; access state via getter.
9. Bloc: no custom public methods; use `add` for communication.
