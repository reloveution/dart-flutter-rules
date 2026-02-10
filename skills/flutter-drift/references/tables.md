---
title: Table Definitions
description: Define database tables in drift
---

## Basic Table Structure

All tables in drift extend the `Table` class and define columns as `late final` fields:

```dart
class TodoItems extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get title => text()();
  DateTimeColumn get createdAt => dateTime().nullable()();
}
```

## Adding Tables to Database

Add tables to your database using the `@DriftDatabase` annotation:

```dart
@DriftDatabase(tables: [TodoItems, Categories])
class AppDatabase extends _$AppDatabase {
  AppDatabase(QueryExecutor e) : super(e);

  @override
  int get schemaVersion => 1;
}
```

## Column Types

| Dart Type | Drift Column | SQL Type |
|------------|---------------|-----------|
| `int` | `integer()` | `INTEGER` |
| `BigInt` | `int64()` | `INTEGER` |
| `String` | `text()` | `TEXT` |
| `bool` | `boolean()` | `INTEGER` (1 or 0) |
| `double` | `real()` | `REAL` |
| `Uint8List` | `blob()` | `BLOB` |
| `DateTime` | `dateTime()` | `INTEGER` or `TEXT` |

## Nullable Columns

Use `nullable()` to allow `null` values:

```dart
late final category = integer().nullable()();
```

## Default Values

### Server Default (SQL)

```dart
late final createdAt = dateTime().withDefault(currentDateAndTime)();
```

### Client Default (Dart)

```dart
late final isActive = boolean().clientDefault(() => true)();
```

## Foreign Keys

Reference another table:

```dart
class Albums extends Table {
  late final artist = integer().references(Artists, #id)();
}

class Artists extends Table {
  late final id = integer().autoIncrement()();
  late final name = text()();
}
```

Enable foreign keys:

```dart
@override
MigrationStrategy get migration {
  return MigrationStrategy(
    beforeOpen: (details) async {
      await customStatement('PRAGMA foreign_keys = ON');
    },
  );
}
```

## Auto Increment Primary Key

```dart
class Items extends Table {
  late final id = integer().autoIncrement()();
  late final title = text()();
}
```

Inserting with auto increment:

```dart
await database.items.insertAll([
  ItemsCompanion.insert(title: 'First entry'),
  ItemsCompanion.insert(title: 'Another item'),
]);
```

## Custom Primary Key

```dart
class Profiles extends Table {
  late final email = text()();

  @override
  Set<Column<Object>> get primaryKey => {email};
}
```

## Unique Columns

Single column unique:

```dart
late final username = text().unique()();
```

Multiple columns unique:

```dart
class Reservations extends Table {
  late final room = text()();
  late final onDay = dateTime()();

  @override
  List<Set<Column>> get uniqueKeys => [
    {room, onDay},
  ];
}
```

## Indexes

Simple index:

```dart
@TableIndex(name: 'user_name', columns: {#name})
class Users extends Table {
  late final id = integer().autoIncrement()();
  late final name = text()();
}
```

Index with ordering:

```dart
@TableIndex(
  name: 'log_entries_at',
  columns: {IndexedColumn(#loggedAt, orderBy: OrderingMode.desc)},
)
class LogEntries extends Table {
  late final loggedAt = dateTime()();
}
```

Custom SQL index:

```dart
@TableIndex.sql('''
  CREATE INDEX pending_orders ON orders (creation_time)
    WHERE status == 'pending';
''')
class Orders extends Table {
  late final status = text()();
  late final creationTime = dateTime()();
}
```

## Table Mixins

Extract common columns:

```dart
mixin TableMixin on Table {
  late final id = integer().autoIncrement()();
  late final createdAt = dateTime().withDefault(currentDateAndTime)();
}

class Posts extends Table with TableMixin {
  late final content = text()();
}
```

## Custom Table Name

```dart
class Products extends Table {
  @override
  String get tableName => 'product_table';
}
```

## Custom Column Name

```dart
late final isAdmin = boolean().named('admin')();
```

## Length Constraints

```dart
late final name = text().withLength(min: 1, max: 50)();
```

## Check Constraints

```dart
late final Column<int> age = integer().check(age.isBiggerOrEqualValue(0))();
```

## Generated Columns

Virtual (computed on read):

```dart
class Squares extends Table {
  late final length = integer()();
  late final width = integer()();
  late final area = integer().generatedAs(length * width)();
}
```

Stored (computed on write):

```dart
class Boxes extends Table {
  late final length = integer()();
  late final width = integer()();
  late final area = integer().generatedAs(length * width, stored: true)();
}
```

## Custom Table Constraints

```dart
class TableWithCustomConstraints extends Table {
  late final foo = integer()();
  late final bar = integer()();

  @override
  List<String> get customConstraints => [
    'FOREIGN KEY (foo, bar) REFERENCES group_memberships ("group", user)',
  ];
}
```

## Strict Tables

```dart
class Preferences extends Table {
  late final key = text()();
  late final value = sqliteAny().nullable()();

  @override
  Set<Column<Object>>? get primaryKey => {key};

  @override
  bool get isStrict => true;
}
```
