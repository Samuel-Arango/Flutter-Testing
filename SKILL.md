---
name: flutter-development
description: Flutter/Dart specialist for mobile apps. Use for pubspec.yaml, widgets, state management, navigation, sqflite/SQLite, architecture, debugging, tests (flutter test). Do NOT use for non-Flutter projects, pure backend, or web-only tasks.
---

# Flutter Development

## Context rules (lean)
- Read only involved files; locate with `glob`/`grep` before `read`.
- Load `references/*` only when needed (see INDEX).
- Reference `path:line`, don't paste large blocks.
- Don't re-analyze the project without reason.

## Mandatory flow
1. Minimal requirements.
2. Inspect only involved files.
3. Implement scoped changes.
4. Unit tests (required, except trivial UI/text changes).
5. Verify services.
6. Verify persistence DB ↔ system.
7. `flutter analyze` + `dart format .` + `flutter test` (or `flutter test --coverage`).

If tests cannot run in the environment, document the blocker and the exact command for the user to run; do not claim "green".

## Layer responsibilities
- Models: data. Repositories: data/SQL. Services: logic. Screens: UI. Widgets: reusable. Core: shared.

## Persistence (SQLite)
- `DatabaseHelper` single; CRUD; parametrized queries; migrations; transactions; errors.
- Consider `shared_preferences` (simple KV), `flutter_secure_storage` (secrets), `drift` (typed/complex queries).
- See `references/persistence/persistence-verification.md`.

## Services
- No UI; injectable; typed errors; tests with mocks.
- See `references/services/services-verification.md`.

## State management
- Default: `Provider` or `Riverpod` if nothing exists. `setState` for local/simple. `Bloc/Cubit` for complex flows. Justify new deps.

## Security/quality
- No plaintext secrets; validate data; parametrized SQL; no unauthorized deletes.

## References (on-demand)
See `references/INDEX.md`. Load only the relevant file.
