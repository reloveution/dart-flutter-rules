---
title: PostgreSQL
description: Use drift with PostgreSQL
---

## Setup

Add PostgreSQL dependencies:

```yaml
dependencies:
  drift: ^2.14.0
  postgres: ^2.6.0
  drift_postgres: ^1.2.0

dev_dependencies:
  drift_dev: ^2.14.0
  build_runner: ^2.4.0
```

## Configure Postgres Dialect

Add to `build.yaml`:

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

## Database Connection

### Simple Connection

```dart
import 'package:drift/drift.dart';
import 'package:drift_postgres/drift_postgres.dart';
import 'package:postgres/postgres.dart';

@DriftDatabase(...)
class AppDatabase extends _$AppDatabase {
  AppDatabase(QueryExecutor e) : super(e);

  @override
  int get schemaVersion => 1;
}

Future<AppDatabase> openPostgresConnection() {
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

### Connection Pool

```dart
import 'package:postgres/postgres_pool.dart';

Future<AppDatabase> openPooledConnection() {
  final pool = PgPool(
      PgEndpoint(
        host: 'localhost',
        port: 5432,
        database: 'mydb',
        username: 'user',
        password: 'password',
      ),
      settings: PoolSettings(
        maxSize: 10,
      ),
    );

  return AppDatabase(PgDatabase.opened(pool));
}
```

### Custom Session

Use existing PostgreSQL session:

```dart
import 'package:postgres/postgres.dart';

Future<AppDatabase> openCustomConnection(Session session) {
  return AppDatabase(PgDatabase.opened(session));
}
```

### Connection Settings

Configure timeouts and options:

```dart
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
        applicationName: 'My Drift App',
      ),
    ),
  );
}
```

## PostgreSQL Types

### UUID Column

```dart
class Users extends Table {
  late final id = postgresUuid().autoGenerate()();
  late final name = text()();
}
```

### JSON Column

```dart
class Settings extends Table {
  late final id = integer().autoIncrement()();
  late final config = postgresJson()();
}
```

### Array Column

```dart
class Posts extends Table {
  late final id = integer().autoIncrement()();
  late final tags = postgresArray(PostgresTypes.text)();
}
```

### Custom Types

Use PostgreSQL-specific types:

```dart
class Data extends Table {
  late final id = integer().autoIncrement()();
  late final metadata = postgresJsonb()();
  late final createdAt = dateTime().withDefault(
    FunctionCallExpression.currentTimestamp(),
  );
}
```

## PostgreSQL Functions

### Generate UUID

```dart
final id = await into(users).insert(
  UsersCompanion.insert(
    name: 'John',
    id: const Value(gen_random_uuid()),
  ),
);
```

### Current Timestamp

```dart
final now = FunctionCallExpression.currentTimestamp();
```

## Queries with PostgreSQL

### JSON Query

```dart
final users = await (select(users)
  ..where((u) =>
      u.jsonData.containsString('key', 'value'))
  ).get();
```

### Array Contains

```dart
final posts = await (select(posts)
  ..where((p) =>
      p.tags.contains('tag1'))
  ).get();
```

### Full Text Search

```dart
final posts = await customSelect('''
    SELECT * FROM posts
    WHERE to_tsvector(content) @@ plainto_tsquery(?)
  ''', ['search term']).get();
```

## Indexes

### JSON Index

```dart
@TableIndex.sql('''
  CREATE INDEX data_key_idx ON data ((config->>'key'))
''')
class Data extends Table {
  late final id = integer().autoIncrement()();
  late final config = postgresJson()();
}
```

### GIN Index for Arrays

```dart
@TableIndex.sql('''
  CREATE INDEX posts_tags_gin ON posts USING GIN (tags)
''')
class Posts extends Table {
  late final id = integer().autoIncrement()();
  late final tags = postgresArray(PostgresTypes.text)();
}
```

## Migrations with PostgreSQL

### Export Schema

Export drift schema for PostgreSQL:

```bash
dart run drift_dev schema dump lib/database.dart > schema.sql
```

### Manual Migrations

Use raw SQL for PostgreSQL migrations:

```dart
from1To2: (m, schema) async {
  await m.customStatement('''
    ALTER TABLE users
    ADD COLUMN created_at TIMESTAMP DEFAULT NOW()
  ''');
}
```

### Migration Tools

Consider PostgreSQL-native tools:
- pgmigrate
- sqitch
- Flyway

## Performance Tips

### Connection Pooling

Always use pools in production:

```dart
final pool = PgPool(endpoint, settings: PoolSettings(maxSize: 20));
final database = AppDatabase(PgDatabase.opened(pool));
```

### Prepared Statements

Drift automatically prepares statements.

### Indexes

Create indexes on frequently queried columns:

```dart
@TableIndex(name: 'users_email_idx', columns: {#email})
class Users extends Table {
  late final email = text()();
}
```

## Testing with PostgreSQL

### Test Database

```dart
import 'package:drift/drift.dart';

AppDatabase createTestDatabase() {
  return AppDatabase(NativeDatabase.memory());
}
```

For PostgreSQL integration tests, use test database:

```dart
AppDatabase createPostgresTestDatabase() {
  final endpoint = HostEndpoint(
      host: 'localhost',
      port: 5432,
      database: 'test_db',
      username: 'test_user',
      password: 'test_pass',
    );

  return AppDatabase(
    PgDatabase(endpoint: endpoint),
  );
}
```

## Common Patterns

### Soft Deletes

```dart
class Todos extends Table {
  late final id = integer().autoIncrement()();
  late final title = text()();
  late final deletedAt = dateTime().nullable()();
}

Future<List<Todo>> getActiveTodos() {
  return (select(todos)
    ..where((t) => t.deletedAt.isNull())
  ).get();
}
```

### Updated At

```dart
class Users extends Table {
  late final id = postgresUuid().autoGenerate()();
  late final name = text()();
  late final updatedAt = dateTime().withDefault(
    FunctionCallExpression.currentTimestamp(),
  );
}
```

## Best Practices

1. **Connection pooling**: Always use pools in production
2. **Indexes**: Index frequently queried columns
3. **Migration tools**: Use PostgreSQL-native tools for complex migrations
4. **Type safety**: Use drift's type generation for PostgreSQL types
5. **Testing**: Use in-memory SQLite for unit tests, real Postgres for integration tests
6. **Timeouts**: Set appropriate connection and query timeouts
7. **SSL**: Enable SSL in production
