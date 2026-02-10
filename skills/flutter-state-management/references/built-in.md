---
title: Flutter Built-in State (Explicit Request Only)
description: Streams, Futures, ValueNotifier
---

# When to Use

When simple state management is explicitly requested or for simple use cases. Do not use a third-party package unless explicitly requested.

# Streams

- Use `Stream`s and `StreamBuilder` for a sequence of asynchronous events

# Futures

- Use `Future`s and `FutureBuilder` for a single asynchronous operation

# ValueNotifier

- Use `ValueNotifier` with `ValueListenableBuilder` for simple, local state involving a single value

```dart
final ValueNotifier<int> _counter = ValueNotifier<int>(0);

ValueListenableBuilder<int>(
  valueListenable: _counter,
  builder: (context, value, child) {
    return Text('Count: $value');
  },
);
```
