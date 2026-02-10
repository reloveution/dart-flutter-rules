---
title: Bloc Ecosystem
description: Packages for persistence, event transformers, undo/redo
---

# Bloc Ecosystem

## Core Packages

- **bloc** – Core state management
- **flutter_bloc** – Flutter widgets (BlocBuilder, BlocProvider, etc.)
- **bloc_test** – Testing
- **bloc_lint** – Linting
- **bloc_tools** – CLI scaffolding

## Extended Packages

- **bloc_concurrency** – Event transformers: sequential, concurrent, droppable, restartable
- **hydrated_bloc** – State persistence and restoration across app sessions
- **replay_bloc** – Undo and redo
- **angular_bloc** – AngularDart support

## Developer Tools

- **Mason** – Custom templates for consistent code generation
- **Bloc DevTools** – Debugging and state inspection

## Usage

Start with bloc and flutter_bloc. Add bloc_concurrency for debounce/throttle. Use hydrated_bloc for persistence. Use replay_bloc for undo/redo.
