---
name: flutter-architecture
description: Comprehensive guide for architecting Flutter applications following MVVM pattern and best practices with feature-first project organization. Use when working with Flutter projects to structure code properly, implement clean architecture layers (UI, Data, Domain), apply recommended design patterns, and organize projects using feature-first approach for scalable, maintainable apps.
---

# Flutter Architecture

## Overview

Provides architectural guidance and best practices for building scalable Flutter applications using MVVM pattern, layered architecture, and recommended design patterns from the Flutter team.

## Reference Files

See detailed documentation for each topic:

- [concepts.md](references/concepts.md) - Core principles (separation of concerns, SSOT, UDF, guidelines)
- [feature-first.md](references/feature-first.md) - Feature-first project organization
- [layers.md](references/layers.md) - Layer responsibilities and interactions
- [mvvm.md](references/mvvm.md) - MVVM pattern in Flutter
- [design-patterns.md](references/design-patterns.md) - Command, Result, Repository, Offline-First
- [layer-dependencies.md](references/layer-dependencies.md) - Dependency chain and constructor interfaces
- [async-design.md](references/async-design.md) - Future-first API for controllers, use cases, repos
- [code-organization.md](references/code-organization.md) - Polymorphism over conditionals, coordination
- [error-handling.md](references/error-handling.md) - Result, runZonedGuarded, multi-level protection

## Project Structure: Feature-First vs Layer-First

Choose the right project organization based on your app's complexity and team size.

### Feature-First (Recommended for teams)

Organize code by business features:

```
lib/
├── features/
│   ├── auth/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   ├── todos/
│   │   ├── data/
│   │   ├── domain/
│   │   └── presentation/
│   └── settings/
│       ├── data/
│       ├── domain/
│       └── presentation/
├── shared/
│   ├── core/
│   ├── data/
│   └── ui/
└── main.dart
```

**When to use:**
- Medium to large apps (10+ features)
- Team development (2+ developers)
- Frequently adding/removing features
- Complex business logic

**Benefits:**
- Features are self-contained units
- Easy to add/remove entire features
- Clear feature boundaries
- Reduced merge conflicts
- Teams work independently on features

See [Feature-First Guide](references/feature-first.md) for complete implementation details.

### Layer-First (Traditional)

Organize code by architectural layers:

```
lib/
├── data/
│   ├── repositories/
│   ├── services/
│   └── models/
├── domain/
│   ├── use-cases/
│   └── entities/
├── presentation/
│   ├── views/
│   └── viewmodels/
└── shared/
```

**When to use:**
- Small to medium apps
- Few features (<10)
- Solo developers or small teams
- Simple business logic

**Benefits:**
- Clear separation by layer
- Easy to find components by type
- Less nesting

## Quick Start

Start with these core concepts:

1. **Separation of concerns** - Split app into UI and Data layers
2. **MVVM pattern** - Use Views, ViewModels, Repositories, and Services
3. **Single source of truth** - Repositories hold the authoritative data
4. **Unidirectional data flow** - State flows from data → logic → UI

For detailed concepts, see [Concepts](references/concepts.md).

## Architecture Layers

Flutter apps should be structured in layers:

- **UI Layer**: Views (widgets) and ViewModels (UI logic)
- **Data Layer**: Repositories (SSOT) and Services (data sources)
- **Domain Layer** (optional): Use-cases for complex business logic

See [Layers Guide](references/layers.md) for detailed layer responsibilities and interactions.

## Core Components

### Views
- Compose widgets for UI presentation
- Contain minimal logic (animations, simple conditionals, routing)
- Receive data from ViewModels
- Pass events via ViewModel commands

### ViewModels
- Transform repository data into UI state
- Manage UI state and commands
- Handle business logic for UI interactions
- Expose state as streams or change notifiers

### Repositories
- Single source of truth for data types
- Aggregate data from services
- Handle caching, error handling, retry logic
- Expose data as domain models

### Services
- Wrap external data sources (APIs, databases, platform APIs)
- Stateless data access layer
- One service per data source

## Design Patterns

Common patterns for robust Flutter apps:

- **Command Pattern** - Encapsulate actions with Result handling
- **Result Type** - Type-safe error handling
- **Repository Pattern** - Abstraction over data sources
- **Offline-First** - Optimistic UI updates with sync

See [Design Patterns](references/design-patterns.md) for implementation details.

## When to Use This Skill

Use this skill when:
- Designing or refactoring Flutter app architecture
- Choosing between feature-first and layer-first project structure
- Implementing MVVM pattern in Flutter
- Creating scalable app structure for teams
- Adding new features to existing architecture
- Applying best practices and design patterns

## Related Project Skills

- **dart-data-patterns** – DTOs, serialization, repositories, sync, architecture (domain vs DTO)
- **dart-dependency-injection** – get_it, composition root, constructor injection
- **dart-design-principles** – SOLID, polymorphism over switch, composition
- **mermaid-diagrams** – Architecture diagrams, flowchart, sequence, state
- **dart-error-handling** – Result type for business logic, exception vs Error
- **dart-resource-management** – Timer, subscriptions, disposal in services/widgets
- **dart-naming-conventions** – Repo, Dts, Ucs suffixes, interface prefixes
- **flutter-bloc** / **flutter-provider** – State management in presentation layer

Project rules: use get_it at composition root only; constructor injection everywhere; DTOs for data transfer; domain entities without DB knowledge.

## Assets

### assets/
- [command.dart](assets/command.dart) - Command pattern template for encapsulating actions
- [result.dart](assets/result.dart) - Result type for safe error handling
- [examples/](assets/examples/) - Code examples showing architecture in practice
