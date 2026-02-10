---
title: Queries
description: SELECT queries in drift
---

## Basic Select

Get all rows from a table:

```dart
final allTodos = await select(todoItems).get();
```

Turn into stream:

```dart
final allTodosStream = select(todoItems).watch();
```

## Where Clause

Filter results with where:

```dart
final completedTodos = await (select(todoItems)
  ..where((t) => t.isCompleted.equals(true))
  ).get();
```

Multiple conditions:

```dart
final filteredTodos = await (select(todoItems)
  ..where((t) => t.isCompleted.equals(true) & t.priority.isBiggerThanValue(3))
  ).get();
```

Operators:
- `equals(value)` - equals
- `isBiggerThan(value)` - greater than
- `isSmallerThan(value)` - less than
- `isBiggerOrEqualValue(value)` - greater or equal
- `isSmallerOrEqualValue(value)` - less or equal
- `like(pattern)` - LIKE operator
- `contains(value)` - contains text
- `isNull()` - IS NULL
- `isNotNull()` - IS NOT NULL

## Limit and Offset

```dart
final pageOfTodos = await (select(todoItems)
  ..limit(20, offset: 40)
  ).get();
```

## Order By

```dart
final sortedTodos = await (select(todoItems)
  ..orderBy([(t) => OrderingTerm(expression: t.createdAt)])
  ).get();
```

Descending order:

```dart
final sortedTodosDesc = await (select(todoItems)
  ..orderBy([
    (t) => OrderingTerm(expression: t.createdAt, mode: OrderingMode.desc)
  ])
  ).get();
```

## Single Row

Get exactly one row:

```dart
final todo = await (select(todoItems)
  ..where((t) => t.id.equals(1))
  ).getSingle();
```

Watch single row as stream:

```dart
final todoStream = (select(todoItems)
  ..where((t) => t.id.equals(1))
  ).watchSingle();
```

Allow null result:

```dart
final todo = await (select(todoItems)
  ..where((t) => t.id.equals(1))
  ).getSingleOrNull();
```

## Mapping

Transform results:

```dart
final titles = await (select(todoItems)
  ..where((t) => t.title.length.isBiggerOrEqualValue(10))
  .map((row) => row.title)
  ).get();
```

## Joins

### Inner Join

```dart
class EntryWithCategory {
  EntryWithCategory(this.entry, this.category);
  final TodoItem entry;
  final Category? category;
}

final results = await (select(todoItems)
  .join([
    innerJoin(categories, categories.id.equalsExp(todoItems.category)),
  ])
  .map((row) => EntryWithCategory(
    row.readTable(todoItems),
    row.readTableOrNull(categories),
  ))
  .get();
```

### Left Outer Join

```dart
final results = await (select(todoItems)
  .join([
    leftOuterJoin(categories, categories.id.equalsExp(todoItems.category)),
  ])
  .map((row) => EntryWithCategory(
    row.readTable(todoItems),
    row.readTableOrNull(categories),
  ))
  .get();
```

### Multiple Joins

```dart
final results = await (select(todoItems)
  .join([
    innerJoin(categories, categories.id.equalsExp(todoItems.category)),
    innerJoin(users, users.id.equalsExp(todoItems.userId)),
  ])
  .get();
```

### Self Join

Join table to itself:

```dart
final otherTodos = alias(todoItems, 'other');

final results = await (select(otherTodos)
  .join([
    innerJoin(
      categories,
      categories.id.equalsExp(otherTodos.category),
      useColumns: false,
    ),
    innerJoin(
      todoItems,
      todoItems.category.equalsExp(categories.id),
      useColumns: false,
    ),
  ])
  .where(todoItems.title.contains('important'))
  .map((row) => row.readTable(otherTodos))
  .get();
```

## Aggregations

### Count

```dart
final count = await (selectOnly(todoItems)
  .addColumns([countAll()])
  .map((row) => row.read(countAll()))
  .getSingle();
```

### Count by Group

```dart
final countPerCategory = await (select(categories)
  .join([
    innerJoin(
      todoItems,
      todoItems.category.equalsExp(categories.id),
      useColumns: false,
    ),
  ])
  ..addColumns([todoItems.id.count()])
  ..groupBy([categories.id])
  .map((row) => (
    category: row.readTable(categories),
    count: row.read(todoItems.id.count())!,
  ))
  .get();
```

### Average

```dart
final avgLength = await (selectOnly(todoItems)
  .addColumns([todoItems.title.length.avg()])
  .map((row) => row.read(todoItems.title.length.avg())!)
  .getSingle();
```

## Subqueries

### In Where Clause

```dart
final latestTodos = await (select(todoItems)
  ..where((t) => t.createdAt.isBiggerThan(
    subqueryExpression(
      selectOnly(todoItems)
        .addColumns([max(todoItems.createdAt)])
        .where((t) => t.userId.equals(currentUserId)),
    ),
  ))
  .get();
```

### From Subquery

```dart
final sub = Subquery(
  select(todoItems)
    ..orderBy([(t) => OrderingTerm.desc(t.createdAt)])
    ..limit(10),
  's',
);

final results = await select(sub).get();
```

## Custom Columns

Add computed column to results:

```dart
final isImportant = todoItems.content.like('%important%');

final results = await select(todoItems)
  .addColumns([isImportant])
  .map((row) => (
    todo: row.readTable(todoItems),
    important: row.read(isImportant)!,
  ))
  .get();
```

## Exists

```dart
final hasTodo = await (selectOnly(todoItems)
  .addColumns([existsQuery(select(todoItems))])
  .map((row) => row.read(existsQuery(select(todoItems)))!)
  .getSingle();
```

## Union

Combine results from multiple queries:

```dart
final query1 = select(todoItems)
  ..where((t) => t.isCompleted.equals(true));

final query2 = select(todoItems)
  ..where((t) => t.priority.equals(1));

final results = await query1.unionAll(query2).get();
```
