---
title: Testing & Configuration
description: Mocks, multiple environments
---

# Testing & Configuration

## Mocks

- Implement proper dependency testing with mocks.
- Constructor injection enables easy mocking: `MyClass(mockService, mockRepository)`.
- No need to override get_it or register mocks globally for unit tests.

## Configuration

- Use proper dependency configuration for different environments.
- Register different implementations for dev/staging/prod.
- Separate setup functions or use parameters to switch implementations.

## Unit Test Example

```dart
test('should do something', () {
  final mockRepo = MockIRepository();
  when(() => mockRepo.get()).thenAnswer((_) async => result);
  final useCase = MyUseCase(mockRepo);
  // test useCase
});
```
