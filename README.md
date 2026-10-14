# Pure.RelationalSchema.Storage.PostgreSQL.Abstractions

PostgreSQL-specific storage abstractions for the **Pure** relational schema ecosystem — an `IStoredSchemaDataSet` that carries its `IDbConnection`.

[![.NET build & check](https://github.com/kudima03/Pure.RelationalSchema.Storage.PostgreSQL.Abstractions/actions/workflows/build-and-check.yml/badge.svg?branch=main)](https://github.com/kudima03/Pure.RelationalSchema.Storage.PostgreSQL.Abstractions/actions/workflows/build-and-check.yml)
[![Build and Deploy](https://github.com/kudima03/Pure.RelationalSchema.Storage.PostgreSQL.Abstractions/actions/workflows/publish-nuget.yml/badge.svg?branch=main)](https://github.com/kudima03/Pure.RelationalSchema.Storage.PostgreSQL.Abstractions/actions/workflows/publish-nuget.yml)
[![NuGet](https://img.shields.io/nuget/v/Pure.RelationalSchema.Storage.PostgreSQL.Abstractions)](https://www.nuget.org/packages/Pure.RelationalSchema.Storage.PostgreSQL.Abstractions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## Overview

`Pure.RelationalSchema.Storage.PostgreSQL.Abstractions` contains the one PostgreSQL-specific contract shared by the PostgreSQL storage packages. It lives in its own interfaces-only package so that the package that implements it and the packages that consume it depend on a small, stable abstraction instead of on each other.

## Public API

| Name | Namespace | Description |
|------|-----------|-------------|
| `IPostgreSqlStoredSchemaDataSet` | `Pure.RelationalSchema.Storage.PostgreSQL.Abstractions` | An `IStoredSchemaDataSet` that also exposes the `IDbConnection Connection` it reads from |

### Who implements and who consumes it

- **Implemented by** `PostgreSqlStoredSchemaDataSet` in `Pure.RelationalSchema.Storage.PostgreSQL.Querying`.
- **Consumed by** `PostgreSqlStoredSchemaDataSetWithInsertedRows` in `Pure.RelationalSchema.Storage.PostgreSQL.Insertion`, which uses the connection to insert rows into the same database.

## Design Principles

- **Interfaces-only** — no implementations, no tests; every file defines exactly one interface
- **AOT-compatible** — `IsAotCompatible=true`

## Dependencies

- [`Pure.RelationalSchema.Storage.Abstractions`](https://github.com/kudima03/Pure.RelationalSchema.Storage.Abstractions/tree/0.1.0-preview.4.1.0) — `IStoredSchemaDataSet` and the other storage interfaces

## Target Frameworks

- .NET 8
- .NET 9
- .NET 10

## Installation

```
dotnet add package Pure.RelationalSchema.Storage.PostgreSQL.Abstractions
```

## Related packages

- `Pure.RelationalSchema.Storage.PostgreSQL.Creation` — creates the schema and tables
- `Pure.RelationalSchema.Storage.PostgreSQL.Querying` — reads rows; implements `IPostgreSqlStoredSchemaDataSet`
- `Pure.RelationalSchema.Storage.PostgreSQL.Insertion` — inserts rows; consumes `IPostgreSqlStoredSchemaDataSet`
