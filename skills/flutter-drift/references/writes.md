---
title: Insert, Update, Delete
description: Write operations in drift
---

## Insert

### Simple Insert

Insert a single row:

```dart
final id = await into(todoItems).insert(
  TodoItemsCompanion.insert(
    title: 'First todo',
    content: 'Some description',
  ),
);
```

Columns with default values or auto-increment can be omitted.

### Insert with Auto Increment

```dart
final id = await into(todoItems).insert(
  TodoItemsCompanion.insert(
    title: 'First todo',
  ),
);
```

### Bulk Insert

```dart
await batch((batch) {
  batch.insertAll(todoItems, [
    TodoItemsCompanion.insert(
      title: 'First entry',
      content: 'My content',
    ),
    TodoItemsCompanion.insert(
      title: 'Another entry',
      content: 'More content',
      category: const Value(3),
    ),
  ]);
});
```

### Upsert (Insert or Update)

Insert if doesn't exist, update if exists:

```dart
final id = await into(users).insertOnConflictUpdate(
  UsersCompanion.insert(
    email: 'user@example.com',
    name: 'John Doe',
  ),
);
```

Requires SQLite 3.24.0+.

### Custom Conflict Target

For upsert with custom unique constraints:

```dart
final id = await into(products).insert(
  ProductsCompanion.insert(
    sku: 'ABC123',
    name: 'Product Name',
  ),
  onConflict: DoUpdate(
    target: [sku],
  ),
);
```

### Insert Returning

Get inserted row with generated values:

```dart
final row = await into(todos).insertReturning(
  TodosCompanion.insert(
    title: 'A todo entry',
    content: 'A description',
  ),
);
```

Requires SQLite 3.35+.

## Update

### Simple Update

Update all matching rows:

```dart
await (update(todoItems)
  ..where((t) => t.id.equals(1))
  .write(TodoItemsCompanion(
    title: const Value('Updated title'),
  ));
```

### Replace

Replace entire row:

```dart
await update(todoItems).replace(
  TodoItem(
    id: 1,
    title: 'Updated title',
    content: 'Updated content',
  ),
);
```

### Partial Update

Only update specific fields:

```dart
await (update(todoItems)
  ..where((t) => t.id.equals(1))
  .write(TodoItemsCompanion(
    title: const Value('Updated title'),
    isCompleted: const Value(true),
  ));
```

### Update with SQL Expression

```dart
await (update(users)
  .write(UsersCompanion.custom(
    name: users.name.lower(),
  ));
```

## Delete

### Delete Matching Rows

```dart
await (delete(todoItems)
  ..where((t) => t.id.equals(1))
  .go();
```

### Delete Multiple

```dart
await (delete(todoItems)
  ..where((t) => t.isCompleted.equals(true))
  .go();
```

### Delete All

```dart
await delete(todoItems).go();
```

### Delete Limit

```dart
await (delete(todoItems)
  ..where((t) => t.id.isSmallerThanValue(10))
  .go();
```

## Companions vs Data Classes

### Data Class (TodoItem)

Holds all fields, represents a full row:

```dart
final todo = TodoItem(
  id: 1,
  title: 'Title',
  content: 'Content',
  createdAt: DateTime.now(),
);
```

### Companion (TodoItemsCompanion)

Used for partial data, updates, and inserts:

```dart
final companion = TodoItemsCompanion(
  title: const Value('Title'),
  content: const Value('Content'),
  createdAt: Value.absent(),
);
```

### Value States

- `Value(value)` - set to this value
- `Value.absent()` - don't update this column
- `const Value(value)` - for non-nullable values

### Important Distinctions

`category: Value(null)` - SET category = NULL
`category: Value.absent()` - don't change category

## Transactions

### Simple Transaction

```dart
await transaction(() async {
  await into(todoItems).insert(
    TodoItemsCompanion.insert(
      title: 'First todo',
    ),
  );

  await into(categories).insert(
    CategoriesCompanion.insert(
      name: 'New Category',
    ),
  );
});
```

### Transaction with Result

```dart
final result = await transaction(() async {
  final id = await into(todoItems).insert(
    TodoItemsCompanion.insert(
      title: 'First todo',
    ),
  );

  await into(categories).insert(
    CategoriesCompanion.insert(
      name: 'New Category',
    ),
  );

  return id;
});
```

### Rollback on Error

```dart
try {
  await transaction(() async {
    await update(todoItems).write(
      TodoItemsCompanion(
        title: const Value('Updated'),
      ),
    );

    await someOtherOperation();
  });
} catch (e) {
  print('Transaction rolled back: $e');
}
```

## Batch Operations

### Batch Insert and Update

```dart
await batch((batch) {
  batch.insertAll(todoItems, [
    TodoItemsCompanion.insert(title: 'First'),
    TodoItemsCompanion.insert(title: 'Second'),
  ]);

  batch.updateAll(todoItems, [
    TodoItemsCompanion(
      id: 1,
      title: const Value('Updated'),
    ),
  ]);
});
```

### Batch with Mixed Operations

```dart
await batch((batch) {
  batch.insert(todoItems, TodoItemsCompanion.insert(title: 'New'));
  batch.update(todoItems, TodoItemsCompanion(
    id: 1,
    title: const Value('Updated'),
  ));
  batch.delete(todoItems, 2);
});
```

## Warning

Always add `where` clause on updates and deletes:

```dart
// BAD - updates ALL rows!
await update(todoItems).write(
  TodoItemsCompanion(
    isCompleted: const Value(true),
  ),
);

// GOOD - only updates matching rows
await (update(todoItems)
  ..where((t) => t.id.equals(1))
  .write(
    TodoItemsCompanion(
      isCompleted: const Value(true),
    ),
  );
```
