---
title: Flutter UI Integration
description: Use drift with Flutter widgets
---

## Provider Setup

Use Provider or Riverpod with drift:

```dart
final databaseProvider = Provider<AppDatabase>((ref) {
  final database = AppDatabase();
  ref.onDispose(database.close);
  return database;
});
```

## StreamBuilder Example

Build reactive UI with drift streams:

```dart
class TodoList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final database = Provider.of<AppDatabase>(context);

    return StreamBuilder<List<TodoItem>>(
      stream: select(database.todoItems).watch(),
      builder: (context, snapshot) {
        if (snapshot.connectionState == ConnectionState.waiting) {
          return const Center(child: CircularProgressIndicator());
        }

        if (snapshot.hasError) {
          return Text('Error: ${snapshot.error}');
        }

        final todos = snapshot.data ?? [];

        if (todos.isEmpty) {
          return const Center(child: Text('No todos yet'));
        }

        return ListView.builder(
          itemCount: todos.length,
          itemBuilder: (context, index) {
            final todo = todos[index];
            return TodoTile(todo: todo);
          },
        );
      },
    );
  }
}
```

## Todo Tile Widget

Interactive list item:

```dart
class TodoTile extends StatelessWidget {
  final TodoItem todo;

  const TodoTile({required this.todo, super.key});

  @override
  Widget build(BuildContext context) {
    final database = Provider.of<AppDatabase>(context);

    return ListTile(
      leading: Checkbox(
        value: todo.isCompleted,
        onChanged: (value) {
          database.update(database.todoItems).replace(
            TodoItem(
              id: todo.id,
              title: todo.title,
              content: todo.content,
              isCompleted: value ?? false,
            ),
          );
        },
      ),
      title: Text(todo.title),
      trailing: IconButton(
        icon: const Icon(Icons.delete),
        onPressed: () {
          database.delete(database.todoItems).go(todo.id);
        },
      ),
    );
  }
}
```

## Add Todo Dialog

Form to add new todos:

```dart
class AddTodoDialog extends StatefulWidget {
  @override
  State<AddTodoDialog> createState() => _AddTodoDialogState();
}

class _AddTodoDialogState extends State<AddTodoDialog> {
  final _controller = TextEditingController();

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    final database = Provider.of<AppDatabase>(context);

    return AlertDialog(
      title: const Text('Add Todo'),
      content: TextField(
        controller: _controller,
        decoration: const InputDecoration(
          labelText: 'Todo title',
        ),
      ),
      actions: [
        TextButton(
          onPressed: () => Navigator.pop(context),
          child: const Text('Cancel'),
        ),
        TextButton(
          onPressed: () async {
            if (_controller.text.isNotEmpty) {
              await database.into(database.todoItems).insert(
                TodoItemsCompanion.insert(
                  title: _controller.text,
                ),
              );
              if (context.mounted) {
                Navigator.pop(context);
              }
            }
          },
          child: const Text('Add'),
        ),
      ],
    );
  }
}
```

## Filtered List

Filter todos by category:

```dart
class FilteredTodoList extends ConsumerWidget {
  final int? categoryId;

  const FilteredTodoList({required this.categoryId, super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final database = ref.watch(databaseProvider);

    return StreamBuilder<List<TodoItem>>(
      stream: (select(database.todoItems)
            ..where((t) => t.category.equals(categoryId))
          ).watch(),
      builder: (context, snapshot) {
        final todos = snapshot.data ?? [];
        return ListView.builder(
          itemCount: todos.length,
          itemBuilder: (context, index) {
            return TodoTile(todo: todos[index]);
          },
        );
      },
    );
  }
}
```

## Search with Debounce

Search with text input:

```dart
class SearchTodoList extends StatefulWidget {
  @override
  State<SearchTodoList> createState() => _SearchTodoListState();
}

class _SearchTodoListState extends State<SearchTodoList> {
  final _searchController = TextEditingController();
  Timer? _debounce;

  @override
  void dispose() {
    _debounce?.cancel();
    _searchController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    final database = Provider.of<AppDatabase>(context);

    return Column(
      children: [
        TextField(
          controller: _searchController,
          decoration: const InputDecoration(
            labelText: 'Search todos',
          ),
          onChanged: (query) {
            _debounce?.cancel();
            _debounce = Timer(
              const Duration(milliseconds: 300),
              () => setState(() {}),
            );
          },
        ),
        Expanded(
          child: StreamBuilder<List<TodoItem>>(
            stream: (select(database.todoItems)
                  ..where((t) =>
                      t.title.contains(_searchController.text))
                ).watch(),
            builder: (context, snapshot) {
              final todos = snapshot.data ?? [];
              return ListView.builder(
                itemCount: todos.length,
                itemBuilder: (context, index) {
                  return TodoTile(todo: todos[index]);
                },
              );
            },
          ),
        ),
      ],
    );
  }
}
```

## Pagination

Paginated list:

```dart
class PaginatedTodoList extends StatefulWidget {
  @override
  State<PaginatedTodoList> createState() => _PaginatedTodoListState();
}

class _PaginatedTodoListState extends State<PaginatedTodoList> {
  final _scrollController = ScrollController();
  final _pageNotifier = ValueNotifier<int>(0);
  final _hasMoreNotifier = ValueNotifier<bool>(true);
  static const _pageSize = 20;

  @override
  void initState() {
    super.initState();
    _scrollController.addListener(_loadMore);
  }

  @override
  void dispose() {
    _scrollController.dispose();
    _pageNotifier.dispose();
    _hasMoreNotifier.dispose();
    super.dispose();
  }

  Future<void> _loadMore() async {
    if (!_scrollController.position.atEdge) return;

    final database = Provider.of<AppDatabase>(context);
    final page = _pageNotifier.value + 1;

    final todos = await (select(database.todoItems)
          ..limit(_pageSize, offset: page * _pageSize)
        ).get();

    if (todos.length < _pageSize) {
      _hasMoreNotifier.value = false;
    }

    _pageNotifier.value = page;
  }

  @override
  Widget build(BuildContext context) {
    final database = Provider.of<AppDatabase>(context);

    return ValueListenableBuilder<int>(
      valueListenable: _pageNotifier,
      builder: (context, page) {
        return FutureBuilder<List<TodoItem>>(
          future: (select(database.todoItems)
                ..limit(_pageSize, offset: page.value * _pageSize)
              ).get(),
          builder: (context, snapshot) {
            if (!snapshot.hasData) {
              return const Center(child: CircularProgressIndicator());
            }

            final todos = snapshot.data!;
            return ListView.builder(
              controller: _scrollController,
              itemCount: todos.length + (_hasMoreNotifier.value ? 1 : 0),
              itemBuilder: (context, index) {
                if (index == todos.length) {
                  return const Center(child: CircularProgressIndicator());
                }
                return TodoTile(todo: todos[index]);
              },
            );
          },
        );
      },
    );
  }
}
```

## Loading States

Handle loading, error, and empty states:

```dart
class TodoListWithStates extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final database = Provider.of<AppDatabase>(context);

    return StreamBuilder<List<TodoItem>>(
      stream: select(database.todoItems).watch(),
      builder: (context, snapshot) {
        switch (snapshot.connectionState) {
          case ConnectionState.waiting:
            return const Center(child: CircularProgressIndicator());

          case ConnectionState.active:
            if (snapshot.data == null) {
              return const Center(child: CircularProgressIndicator());
            }
            return _buildList(snapshot.data!);

          case ConnectionState.done:
            if (snapshot.hasError) {
              return ErrorWidget(
                message: snapshot.error.toString(),
                onRetry: () {
                  // Force reload
                },
              );
            }
            if (snapshot.data == null || snapshot.data!.isEmpty) {
              return const EmptyStateWidget(
                message: 'No todos yet',
                icon: Icons.checklist,
              );
            }
            return _buildList(snapshot.data!);

          default:
            return const SizedBox.shrink();
        }
      },
    );
  }

  Widget _buildList(List<TodoItem> todos) {
    return ListView.builder(
      itemCount: todos.length,
      itemBuilder: (context, index) {
        return TodoTile(todo: todos[index]);
      },
    );
  }
}
```

## Pull to Refresh

Refresh data with pull-to-refresh:

```dart
class RefreshableTodoList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final database = Provider.of<AppDatabase>(context);

    return RefreshIndicator(
      onRefresh: () async {
        // Stream will emit new data automatically
        await Future.delayed(const Duration(milliseconds: 500));
      },
      child: StreamBuilder<List<TodoItem>>(
        stream: select(database.todoItems).watch(),
        builder: (context, snapshot) {
          final todos = snapshot.data ?? [];
          return ListView.builder(
            itemCount: todos.length,
            itemBuilder: (context, index) {
              return TodoTile(todo: todos[index]);
            },
          );
        },
      ),
    );
  }
}
```

## Best Practices

1. **Close database**: Always close database on dispose
2. **Stream cleanup**: Cancel streams when widget unmounts
3. **Debounce user input**: Use timers for search/typing
4. **Handle errors**: Show user-friendly error messages
5. **Loading states**: Show appropriate loading indicators
6. **Pagination**: Use limit/offset for large datasets
7. **Optimize queries**: Index frequently filtered columns
8. **Avoid unnecessary rebuilds**: Use Provider/Riverpod selectively
