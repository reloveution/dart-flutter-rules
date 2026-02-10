---
title: Architecture Principles
description: Domain vs DTO, layer boundaries
---

# Architecture Principles

## Domain and Database

- Domain entities must have no knowledge of the database.
- Domain layer stays pure; no JSON, no SQL, no platform APIs.

## DTO Responsibilities

- DTO models encapsulate all mapping and JSON conversion logic.
- Convert between external format and domain entity in repository/data layer.

## Table Definitions

- Table definitions should reference only DTOs.
- Do not reference converters in table definitions.
- Keep persistence model (DTO) separate from domain model.

## Layer Boundaries

- Data layer owns serialization and persistence.
- Domain layer owns business rules and entities.
- Presentation layer consumes domain or DTO projections as needed.
