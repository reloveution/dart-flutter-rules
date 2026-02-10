# go_router Guide

## Basic Setup

Add to `pubspec.yaml`:
```yaml
dependencies:
  go_router: ^17.0.0
```

## Simple Configuration

```dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';

final _router = GoRouter(
  routes: [
    GoRoute(path: '/', builder: (context, state) => HomeScreen()),
    GoRoute(path: '/details', builder: (context, state) => DetailsScreen()),
  ],
);

void main() {
  runApp(MaterialApp.router(routerConfig: _router));
}
```

## Navigation Methods

### Declarative Navigation

**Go to screen (replace current):**
```dart
context.go('/details');
```

**Push screen (add to stack):**
```dart
context.push('/details');
```

**Pop screen (go back):**
```dart
context.pop();
// OR return data
context.pop('result_value');
```

### Named Routes with go_router

```dart
GoRoute(
  name: 'details',
  path: '/details/:id',
  builder: (context, state) {
    final id = state.pathParameters['id'];
    return DetailsScreen(id: id!);
  },
);

// Navigate using name
context.goNamed('details', pathParameters: {'id': '123'});
// With query parameters
context.goNamed('details', 
  pathParameters: {'id': '123'},
  queryParameters: {'tab': 'info'},
);
```

## Passing Data

### Path Parameters
```dart
GoRoute(path: '/users/:userId', builder: (context, state) {
  final userId = state.pathParameters['userId'];
  return UserDetailScreen(userId: userId!);
});

context.push('/users/123');
```

### Query Parameters
```dart
GoRoute(path: '/search', builder: (context, state) {
  final query = state.queryParameters['q'];
  final page = state.queryParameters['page'];
  return SearchScreen(query: query, page: int.tryParse(page ?? '1'));
});

context.push('/search?q=flutter&page=2');
// OR using queryParameters parameter
context.push('/search', queryParameters: {'q': 'flutter', 'page': '2'});
```

### Extra Data
```dart
GoRoute(path: '/details', builder: (context, state) {
  final extra = state.extra as Map<String, dynamic>?;
  return DetailsScreen(data: extra);
});

context.push('/details', extra: {'key': 'value'});
// Can combine with query parameters
context.push('/details', 
  extra: {'key': 'value'},
  queryParameters: {'id': '123'},
);
```

## Advanced Patterns

### Nested Routes (Shell Routes)

```dart
ShellRoute(
  builder: (context, state, child) {
    return Scaffold(
      appBar: AppBar(title: const Text('App')),
      body: child,
      bottomNavigationBar: BottomNavigationBar(
        items: const [
          BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
          BottomNavigationBarItem(icon: Icon(Icons.settings), label: 'Settings'),
        ],
        onTap: (index) {
          if (index == 0) context.go('/home');
          if (index == 1) context.go('/settings');
        },
      ),
    );
  },
  routes: [
    GoRoute(path: '/home', builder: (context, state) => HomeScreen()),
    GoRoute(path: '/settings', builder: (context, state) => SettingsScreen()),
  ],
);
```

### Route Guards (Redirects)

```dart
GoRouter(
  redirect: (context, state) {
    final isAuthenticated = checkAuth();
    final isLoggingIn = state.matchedLocation == '/login';

    if (!isAuthenticated && !isLoggingIn) {
      return '/login';
    }
    if (isAuthenticated && isLoggingIn) {
      return '/';
    }
    return null; // no redirect
  },
  routes: [...],
);
```

### Error Handling

```dart
GoRouter(
  errorBuilder: (context, state) => ErrorScreen(error: state.error),
  routes: [...],
);
```

## Deep Linking

go_router automatically handles deep linking. Ensure platform setup:

**Android** (`AndroidManifest.xml`):
```xml
<intent-filter>
  <action android:name="android.intent.action.VIEW" />
  <category android:name="android.intent.category.DEFAULT" />
  <category android:name="android.intent.category.BROWSABLE" />
  <data android:scheme="https" android:host="yourapp.com" />
</intent-filter>
```

**iOS** (`Info.plist`):
```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>yourapp</string>
    </array>
  </dict>
</array>
```

## Common Pitfalls

1. **Don't use `Navigator.push/pop` directly** when using go_router for main navigation
2. **Always check `context.mounted`** after async navigation operations
3. **Use `context.push()`** for adding to stack, `context.go()` for replacing
4. **Path parameters are mandatory**, query parameters are optional
5. **Web browser back button works automatically** with go_router
6. **API changes in v7.0.0+**: Use `pathParameters`/`queryParameters` instead of `params`/`queryParams`, and `matchedLocation` instead of `subloc`
7. **Use `ShellRoute`** for nested navigation with persistent UI, not nested `GoRoute` with `Navigator`