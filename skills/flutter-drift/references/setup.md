---
title: Setup
description: Setup drift for Flutter applications
---

## Dependencies

Add drift to your `pubspec.yaml`:

```yaml
dependencies:
  drift: ^2.30.0
  drift_flutter: ^0.2.8
  path_provider: ^2.1.5

dev_dependencies:
  drift_dev: ^2.30.0
  build_runner: ^2.10.4
```

Or run:

```bash
dart pub add drift drift_flutter path_provider dev:drift_dev dev:build_runner
```

## Web Support

Running sqlite3 on the web requires additional sources that must be downloaded into the `web/` folder:
- `sqlite3.wasm` module
- `drift_worker.js` worker

Obtain these files and place them in your `web/` directory.

## Database Class

Every Flutter app using drift needs a database class. Create a `database.dart` file:

```dart
import 'package:drift/drift.dart';
import 'package:drift_flutter/drift_flutter.dart';

part 'database.g.dart';

// Define tables
class TodoItems extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get title => text()();
  DateTimeColumn get createdAt => dateTime().nullable()();
}

@DriftDatabase(tables: [TodoItems])
class AppDatabase extends _$AppDatabase {
  AppDatabase([QueryExecutor? e])
      : super(
          e ??
              driftDatabase(
                name: 'app_db',
                native: const DriftNativeOptions(
                  databaseDirectory: getApplicationSupportDirectory,
                ),
                web: DriftWebOptions(
                  sqlite3Wasm: Uri.parse('sqlite3.wasm'),
                  driftWorker: Uri.parse('drift_worker.js'),
                ),
              ),
        );

  @override
  int get schemaVersion => 1;
}
```

## Manual Database Setup

If you need more control over database opening:

```dart
import 'package:drift/drift.dart';
import 'package:path_provider/path_provider.dart';
import 'package:sqlite3_flutter_libs/sqlite3_flutter_libs.dart';

Future<DatabaseConnection> openConnection() async {
  final dbFolder = await getApplicationDocumentsDirectory();
  final file = File(p.join(dbFolder.path, 'db.sqlite'));

  if (Platform.isAndroid) {
    await applyWorkaroundToOpenSqlite3OnOldAndroidVersions();
  }

  final cachebase = await getTemporaryDirectory();
  await sqlite3FlutterLibsInit();

  return NativeDatabase.createInBackground(file);
}
```

## Sharing Databases Between Isolates

Enable isolate sharing:

```dart
AppDatabase.defaults(): super(
  driftDatabase(
    name: 'app_db',
    native: DriftNativeOptions(
      shareAcrossIsolates: true,
    ),
  ),
);
```

## Running the Code Generator

Generate code with build_runner:

```bash
dart run build_runner build
```

Or watch for changes during development:

```bash
dart run build_runner watch
```
