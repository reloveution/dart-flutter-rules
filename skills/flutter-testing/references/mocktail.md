# Mocktail Mocking Guide

Project uses Mocktail (not Mockito) for mocks. Follow these rules when mocking dependencies.

## Rules

1. **Fake vs Mock**: Use Fake when asserting outcomes; use Mock when verifying interactions.
2. **Mock creation**: Extend `Mock`, no manual overrides in subclass.
3. **Fallback values**: Call `registerFallbackValue` for every non-nullable custom type used in matchers, before stubbing/verifying.
4. **Stubbing sync**: `when(() => mock.method()).thenReturn(value)` or `thenAnswer((i) => value)` for dynamic; `thenThrow(error)` for failures.
5. **Stubbing async**: Always return `Future` via `thenAnswer((_) async => result)` or `thenReturn(Future.value(result))`.
6. **Verification**: Use `verify(() => ...)`, `verifyNever(() => ...)`, `verify(() => ...).called(n)`.
7. **Named params**: Supply all in stubs/verifies; use `any(named: 'param')` when value irrelevant.
8. **Matchers**: `any()`, `captureAny()`, `captureThat()` for flexible matching.
9. **Prefer real/fakes** when asserting outcomes, not interaction patterns.
10. **Stub every** dependency method expected in test to avoid MissingStub.
11. **toString**: Ensure types have deterministic toString for equals-based assertions.

## Example

```dart
class MockRepo extends Mock implements IRepository {}

void main() {
  late MockRepo mockRepo;

  setUpAll(() {
    registerFallbackValue(SomeType());
  });

  setUp(() {
    mockRepo = MockRepo();
  });

  test('fetches data', () async {
    when(() => mockRepo.getData()).thenAnswer((_) async => Result.success(data));
    final result = await useCase.execute();
    verify(() => mockRepo.getData()).called(1);
  });
}
```
