---
title: GoRouter and Navigation
description: GoRouter setup, Navigator
---

# When Project Uses GoRouter

- Use `go_router` for declarative navigation, deep linking, web support
- Configure `redirect` for authentication flows
- Use Navigator for short-lived screens (dialogs, temporary views) that don't need deep linking

# GoRouter Setup

```dart
final GoRouter _router = GoRouter(
  routes: <RouteBase>[
    GoRoute(
      path: '/',
      builder: (context, state) => const HomeScreen(),
      routes: <RouteBase>[
        GoRoute(
          path: 'details/:id',
          builder: (context, state) {
            final String id = state.pathParameters['id']!;
            return DetailScreen(id: id);
          },
        ),
      ],
    ),
  ],
);

MaterialApp.router(routerConfig: _router);
```

# Navigator (Dialogs, Short-lived)

- `Navigator.push` for new screen
- `Navigator.pop` to go back
- Prefer GoRouter, AutoRouter, Navigator 2.0 over Navigator.push/pop for main navigation
