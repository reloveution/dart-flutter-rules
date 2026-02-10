---
title: Stream Queries
description: Watch queries in drift
---

## Basic Stream

Watch query results:

```dart
final todosStream = select(todoItems).watch();
```

Use with StreamBuilder in Flutter:

```dart
StreamBuilder<List<TodoItem>>(
  stream: select(todoItems).watch(),
  builder: (context, snapshot) {
    if (!snapshot.hasData) {
      return CircularProgressIndicator();
    }

    final todos = snapshot.data!;
    return ListView.builder(
      itemCount: todos.length,
      itemBuilder: (context, index) {
        return ListTile(
          title: Text(todos[index].title),
        );
      },
    );
  },
)
```

## Stream Single Item

Watch single row:

```dart
final todoStream = (select(todoItems)
  ..where((t) => t.id.equals(1))
  .watchSingle();
```

Or allow null:

```dart
final todoStream = (select(todoItems)
  ..where((t) => t.id.equals(1))
  .watchSingleOrNull();
```

## Get vs Watch

Run once vs watch continuously:

```dart
// Run once, get current results
final todos = await select(todoItems).get();

// Watch for changes, get updates
final todosStream = select(todoItems).watch();
```

## StreamBuilder Usage

Complete StreamBuilder example:

```dart
class TodoList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final database = Provider.of<AppDatabase>(context);

    return StreamBuilder<List<TodoItem>>(
      stream: select(todoItems).watch(),
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return CircularProgressIndicator();
        }

        if (snapshot.hasError) {
          return Text('Error: ${snapshot.error}');
        }

        final todos = snapshot.data ?? [];

        if (todos.isEmpty) {
          return Center(child: Text('No todos yet'));
        }

        return ListView.builder(
          itemCount: todos.length,
          itemBuilder: (context, index) {
            final todo = todos[index];
            return ListTile(
              title: Text(todo.title),
              trailing: Checkbox(
                value: todo.isCompleted,
                onChanged: (value) {
                  database.update(todoItems).replace(
                    TodoItem(
                      id: todo.id,
                      title: todo.title,
                      isCompleted: value ?? false,
                    ),
                  );
                },
              ),
            );
          },
        );
      },
    );
  }
}
```

## Riverpod Integration

Wrap stream with StreamProvider:

```dart
final todosProvider = StreamProvider.autoDispose<List<TodoItem>>((ref) {
  final database = ref.watch(databaseProvider);
  return select(database.todoItems).watch();
});
```

Use in widget:

```dart
class TodoList extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final todos = ref.watch(todosProvider);

    return ListView.builder(
      itemCount: todos.length,
      itemBuilder: (context, index) {
        return ListTile(title: Text(todos[index].title));
      },
    );
  }
}
```

## Watch Filtered Results

Watch filtered query:

```dart
final activeTodos = (select(todoItems)
  ..where((t) => !t.isCompleted)
  .watch();
```

Watch sorted results:

```dart
final sortedTodos = (select(todoItems)
  ..orderBy([(t) => OrderingTerm.desc(t.createdAt)])
  .watch();
```

## Watch with Joins

Watch joined query results:

```dart
class EntryWithCategory {
  EntryWithCategory(this.entry, this.category);
  final TodoItem entry;
  final Category? category;
}

final todosWithCategoryStream = (select(todoItems)
  .join([
      leftOuterJoin(categories, categories.id.equalsExp(todoItems.category)),
    ])
  .map((row) => EntryWithCategory(
        row.readTable(todoItems),
        row.readTableOrNull(categories),
      ))
  .watch();
```

## Custom Query Streams

Watch custom SQL query:

```dart
Stream<List<TodoItem>> watchCompletedTodos() {
  return watch('''
    SELECT * FROM todo_items
    WHERE is_completed = ?
    ORDER BY created_at DESC
  ''', [true]);
}
```

## Table Update Events

Listen to table updates directly:

```dart
final todoUpdates = todoUpdates(todoItems).listen((event) {
  switch (event.kind) {
    case UpdateKind.insert:
      print('New todo inserted: ${event.row}');
    case UpdateKind.update:
      print('Todo updated: ${event.row}');
    case UpdateKind.delete:
      print('Todo deleted');
  }
});
```

## Manual Update Trigger

Trigger stream updates manually:

```dart
void triggerUpdates() {
  notifyTableUpdates(todoItems);
}
```

## Stream Cancellation

Cancel stream subscription:

```dart
StreamSubscription? subscription;

void startWatching() {
  subscription = select(todoItems).watch().listen((todos) {
    print('Updated todos: $todos');
  });
}

void stopWatching() {
  subscription?.cancel();
  subscription = null;
}
```

## Stream Debouncing

Debounce rapid updates:

```dart
import 'dart:async';

Stream<List<TodoItem>> watchDebouncedTodos() {
  return select(todoItems).watch().debounceTime(
    const Duration(milliseconds: 300),
  );
}
```

## Stream Transformation

Transform stream data:

```dart
final todoTitles = select(todoItems)
  .watch()
  .map((todos) => todos.map((t) => t.title).toList());

final activeCount = (select(todoItems)
  ..where((t) => !t.isCompleted)
  .watch()
  .map((todos) => todos.length);
```

## Stream Error Handling

Handle stream errors:

```dart
select(todoItems).watch().listen(
  (todos) {
    // Handle new data
    updateUI(todos);
  },
  onError: (error, stack) {
    // Handle errors
    showError(error);
  },
  onDone: () {
    // Stream closed
    print('Stream closed');
  },
);
```

## Limitations

Streams have these limitations:

1. **External changes**: Updates made outside of drift APIs don't trigger stream updates
2. **Coarse updates**: Streams update for any change to watched tables, not just relevant rows
3. **Performance**: Stream queries should be efficient (few rows, fast execution)

## Best Practices

- Use streams for UI-reactive data (lists, counters)
- Prefer `watch()` over repeated `get()` calls
- Keep stream queries efficient (limit rows, use indexes)
- Cancel stream subscriptions when not needed
- Use `watchSingle()` for single-item queries
- Filter and map streams as needed for UI requirements
