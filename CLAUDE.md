# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

All `dotnet` commands must be run from the `./src` directory.

```bash
dotnet restore
dotnet build --no-restore -warnaserror
dotnet format --verify-no-changes             # check code style (CI enforces this)
dotnet format                                 # auto-fix code style
dotnet tool restore && dotnet csharpier check .   # CI enforces this too
dotnet pack --configuration Release -p:Version=<version> --output .
```

CI additionally passes `-p:AssemblyVersion` (pinned to the major) and `-p:FileVersion`; see `.github/workflows/publish-nuget.yml`.

There are no test or benchmark projects — the CI pipeline (`build-and-check.yml`) only builds and checks formatting.

## Architecture

This is an **interfaces-only NuGet library** — no implementations, no tests. Every file defines exactly one interface.

**Interface:**

- `IPostgreSqlStoredSchemaDataSet` — extends `IStoredSchemaDataSet` (from `Pure.RelationalSchema.Storage.Abstractions`, a read-only dictionary of `ITable` → `IStoredTableDataSet` that carries its `ISchema`) and adds `IDbConnection Connection`.

It is implemented by `PostgreSqlStoredSchemaDataSet` in `Pure.RelationalSchema.Storage.PostgreSQL.Querying` and consumed by `Pure.RelationalSchema.Storage.PostgreSQL.Insertion`.

**Multi-targeting:** net7.0, net8.0, net9.0, net10.0. All interfaces must remain AOT-compatible (`IsAotCompatible=true`).

**Package validation:** `EnablePackageValidation = true`. There is no `PackageValidationBaselineVersion` until the first release; set it afterwards. Breaking API changes then fail the build.

**Publishing:** triggered by pushing a semver tag matching `*.*.*`. The tag name becomes the `PackageVersion`. Packages are published to both GitHub Packages and NuGet.org.

## Code Style

Enforced via `.editorconfig`, `dotnet format --verify-no-changes` and `csharpier` in CI:

- No `var` — always use explicit types
- No expression-bodied methods or constructors — properties, indexers, accessors, and lambdas may be expression-bodied
- File-scoped namespace declarations
- Private fields prefixed with `_` (underscore camelCase)
- No non-private instance fields
- `using` directives outside the namespace, System directives sorted first
- Max line length: 90 characters
- Braces on new lines (`csharp_new_line_before_open_brace = all`)
- No implicit object creation (`new()` without type) when the type is apparent

## Commit Messages

Do not mention Claude or AI assistance in commit messages.
