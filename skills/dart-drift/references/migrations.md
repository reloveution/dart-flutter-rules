---
title: Migrations
description: Database migrations in drift
---

## Configure for Migrations

Add database to `build.yaml`:

```yaml
targets:
  $default:
    builders:
      drift_dev:
        options:
          databases:
            my_database: lib/database.dart
            another_db: lib/database2.dart

          schema_dir: drift_schemas/
          test_dir: test/drift/
```

## Run Migration Generator

```bash
dart run drift_dev make-migrations
```

This generates:
- `database.steps.dart` - step-by-step migration helper
- Test files for migration verification
- Schema files for each version

## Step-by-Step Migrations

Use generated `stepByStep` function:

```dart
import 'database.steps.dart';

@DriftDatabase(...)
class AppDatabase extends _$AppDatabase {
  @override
  int get schemaVersion => 3;

  @override
  MigrationStrategy get migration {
    return MigrationStrategy(
        onUpgrade: stepByStep(
          from1To2: (m, schema) async {
            // Version 1 to 2: Add column
            await m.addColumn(schema.todoItems, schema.todoItems.dueDate);
          },
          from2To3: (m, schema) async {
            // Version 2 to 3: Add indexes and alter table
            await m.create(schema.todosDelete);
            await m.create(schema.todosUpdate);
            await m.alterTable(TableMigration(schema.todoItems));
          },
        ),
      );
  }
}
```

## Common Migration Operations

### Add Column

```dart
from1To2: (m, schema) async {
  await m.addColumn(schema.users, schema.users.birthDate);
}
```

### Drop Column

```dart
from2To3: (m, schema) async {
  await m.dropColumn(schema.users, schema.users.oldField);
}
```

### Rename Column

```dart
from1To2: (m, schema) async {
  await m.renameColumn(schema.users, schema.users.name, schema.users.fullName);
}
```

### Add Table

```dart
from1To2: (m, schema) async {
  await m.createTable(schema.categories);
}
```

### Drop Table

```dart
from2To3: (m, schema) async {
  await m.deleteTable('users');
}
```

### Alter Table

Rebuild table with new constraints:

```dart
from2To3: (m, schema) async {
  await m.alterTable(TableMigration(schema.todoItems));
}
```

### Create Index

```dart
from1To2: (m, schema) async {
  await m.create(schema.usersByNameIndex);
}
```

### Drop Index

```dart
from2To3: (m, schema) async {
  await m.dropIndex('users_name_idx');
}
```

### Custom SQL

Execute custom SQL:

```dart
from1To2: (m, schema) async {
  await m.customStatement('''
    UPDATE users
    SET status = 'inactive'
    WHERE last_login < ?
  ''', [DateTime.now().subtract(Duration(days: 365)]);
}
```

## Post-Migration Callbacks

Run code after migrations:

```dart
@override
MigrationStrategy get migration {
  return MigrationStrategy(
      onUpgrade: stepByStep(...),
      beforeOpen: (details) async {
        // Enable foreign keys
        await customStatement('PRAGMA foreign_keys = ON');

        // Populate default data
        if (details.wasCreated) {
          final workId = await into(categories).insert(
            CategoriesCompanion.insert(
              name: 'Work',
            ),
          );

          await into(todoItems).insert(
            TodoItemsCompanion.insert(
              title: 'First todo',
              category: Value(workId),
            ),
          );
        }
      },
    );
}
```

## Manual Migrations

Write migrations without `make-migrations`:

```dart
@override
MigrationStrategy get migration {
  return MigrationStrategy(
      onCreate: (Migrator m) async {
        await m.createAll();
      },
      onUpgrade: (Migrator m, int from, int to) async {
        if (from == 1 && to == 2) {
          await m.addColumn(todoItems, todoItems.dueDate);
        }
        if (from == 2 && to == 3) {
          await m.create(todosDelete);
        }
      },
    );
}
```

## Testing Migrations

Generated test files verify migrations:

```bash
dart test test/drift/schema_test.dart
```

Test validates:
- Data integrity across migrations
- Schema consistency
- Migration correctness

## Data Migration Strategies

### Copy and Transform

Migrate data with transformation:

```dart
from1To2: (m, schema) async {
  // Add new column
  await m.addColumn(schema.users, schema.users.fullName);

  // Transform data
  final users = await (select(users)).get();
  await batch((batch) {
    for (final user in users) {
      batch.update(
        users,
        UsersCompanion(
          id: Value(user.id),
          fullName: Value('${user.firstName} ${user.lastName}'),
        ),
      );
    }
  });
}
```

### Rename with Data Migration

```dart
from1To2: (m, schema) async {
  // Rename column
  await m.renameColumn(schema.users, schema.users.name, schema.users.username);

  // Migrate data if needed
  await customStatement('''
    UPDATE users
    SET username = LOWER(name)
    WHERE username IS NULL
  ''');
}
```

## Debugging Migrations

### Enable Logging

```dart
@override
MigrationStrategy get migration {
  return MigrationStrategy(
      onUpgrade: stepByStep(...),
      beforeOpen: (details) async {
        print('Opening database, version: ${details.to}');
        print('Was created: ${details.wasCreated}');
      },
    );
}
```

### Check Current Schema

```dart
Future<void> debugSchema() async {
  final executor = database.executor;
  final schema = await database.schema;
  print('Current schema: $schema');
}
```

## Common Patterns

### Add Foreign Key

```dart
from1To2: (m, schema) async {
  await m.addColumn(schema.todoItems, schema.todoItems.category);
}

// Re-enable after migration
@override
MigrationStrategy get migration {
  return MigrationStrategy(
      onUpgrade: stepByStep(...),
      beforeOpen: (details) async {
        if (details.hadUpgrade) {
          await customStatement('PRAGMA foreign_keys = ON');
        }
      },
    );
}
```

### Rename Table

```dart
from1To2: (m, schema) async {
  await m.createTable(schema.newUsers);
  await m.customStatement('''
    INSERT INTO new_users
    SELECT * FROM old_users
  ''');
  await m.deleteTable('old_users');
}
```

### Add Unique Constraint

```dart
from1To2: (m, schema) async {
  await m.alterTable(
        TableMigration(
          schema.users,
          newColumns: {schema.users.email.unique()},
        ),
      );
}
```

## Best Practices

1. **Incremental migrations**: Use `stepByStep` for maintainable code
2. **Test thoroughly**: Run generated tests for each migration
3. **Backup data**: Ensure migrations don't lose user data
4. **Use transactions**: Wrap data migrations in transactions
5. **Document changes**: Comment complex transformations
6. **Version carefully**: Only bump `schemaVersion` when schema changes
