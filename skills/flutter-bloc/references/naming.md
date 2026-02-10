---
title: Naming Conventions
description: Event and state naming for Bloc and Cubit
---

# Naming Conventions

## Events

1. Name events in the past tense (actions that have already occurred from bloc's perspective).
2. Format: `BlocSubject + optional noun + verb`. Examples: `LoginButtonPressed`, `UserProfileLoaded`.
3. For initial load events: `BlocSubjectStarted`. Example: `AuthenticationStarted`.
4. Base event class: `BlocSubjectEvent`.

## States

5. Name states as nouns (state is a snapshot at a point in time).
6. Subclasses format: `BlocSubject + Initial | Success | Failure | InProgress`. Examples: `LoginInitial`, `LoginSuccess`, `LoginFailure`, `LoginInProgress`.
7. Single-class format: `BlocSubjectState` with `BlocSubjectStatus` enum (initial, success, failure, loading). Example: `LoginState` with `LoginStatus.initial`.
8. Base state class: always `BlocSubjectState`.
