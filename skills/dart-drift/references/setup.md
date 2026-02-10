---
title: Setup
description: Setup drift for Dart applications
---

## SQLite Setup

Add drift to your `pubspec.yaml`:

```yaml
dependencies:
  drift: ^2.14.0
  sqlite3: ^2.4.0

dev_dependencies:
  drift_dev: ^2.14.0
  build_runner: ^2.4.0
```

Or run:

```bash
dart pub add drift sqlite3 dev:drift_dev dev:build_runner
```

## PostgreSQL Setup

For PostgreSQL databases, add these dependencies:

```yaml
dependencies:
  drift: ^2.14.0
  postgres: ^2.6.0
  drift_postgres: ^1.2.0

dev_dependencies:
  drift_dev: ^2.14.0
  build_runner: ^2.4.0
```

Or run:

```bash
dart pub add drift postgres drift_postgres dev:drift_dev dev:build_runner
```

Configure for PostgreSQL in `build.yaml`:

```yaml
targets:
  $default:
    builders:
      drift_dev:
        options:
          sql:
            dialects:
              - postgres
```

## Database Class (SQLite)

Every Dart app using drift needs a database class. Create a `database.dart` file:

```dart
import 'package:drift/drift.dart';

part 'database.g.dart';

class TodoItems extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get title => text()();
  DateTimeColumn get createdAt => dateTime().nullable()();
}

@DriftDatabase(tables: [TodoItems])
class AppDatabase extends _$AppDatabase {
  AppDatabase(QueryExecutor e) : super(e);

  @override
  int get schemaVersion => 1;
}
```

## Opening Database (SQLite)

```dart
import 'package:drift/drift.dart';
import 'package:sqlite3/sqlite3.dart';
import 'package:path/path.dart';

AppDatabase openConnection() {
  final file = File('db.sqlite');
  return AppDatabase(LazyDatabase(() async {
    final db = sqlite3.open(file.path);
    return NativeDatabase.createInBackground(db);
  });
}
```

## Opening Database (PostgreSQL)

```dart
import 'package:drift/drift.dart';
import 'package:drift_postgres/drift_postgres.dart';
import 'package:postgres/postgres.dart';

AppDatabase openPostgresConnection() {
  final endpoint = HostEndpoint(
    host: 'localhost',
    port: 5432,
    database: 'mydb',
    username: 'user',
    password: 'password',
  );

  return AppDatabase(
    PgDatabase(
      endpoint: endpoint,
    ),
  );
}
```

## Connection Pooling (PostgreSQL)

For better performance with PostgreSQL:

```dart
AppDatabase openPooledPostgresConnection() {
  final endpoint = HostEndpoint(
    host: 'localhost',
    port: 5432,
    database: 'mydb',
    username: 'user',
    password: 'password',
  );

  return AppDatabase(
    PgDatabase(
      endpoint: endpoint,
      settings: ConnectionSettings(
        connectTimeout: Duration(seconds: 10),
        queryTimeout: Duration(seconds: 30),
      ),
    ),
  );
}
```

## In-Memory Database (Testing)

For unit tests, use an in-memory database:

```dart
AppDatabase createTestDatabase() {
  return AppDatabase(NativeDatabase.memory());
}
```

## Running Code Generator

Generate code with build_runner:

```bash
dart run build_runner build
```

Or watch for changes during development:

```bash
dart run build_runner watch
```
