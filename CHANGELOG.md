# Changelog

All notable changes to `Pure.RelationalSchema.Storage.PostgreSQL.Abstractions` are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- `net7.0` target framework.
- `TrimmedHash` — an `IString` that truncates a hash to 63 characters, the PostgreSQL identifier length limit. Moved from `Pure.RelationalSchema.Storage.PostgreSQL.Insertion`.

## [0.1.0-preview.0.1.0] — 2026-10-14

### Added

- Initial release: `IPostgreSqlStoredSchemaDataSet`, moved from `Pure.RelationalSchema.Storage.PostgreSQL` 0.1.0-preview.8.1.2.
