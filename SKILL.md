---
name: flutter-development
description: Especialista Flutter/Dart. Usar para UI, estado, navegación, SQLite, arquitectura, depuración y pruebas. Prioriza contexto mínimo, pruebas unitarias obligatorias, verificación de servicios y persistencia BD.
---

# Flutter Development

## Reglas de contexto (lean)
- Lee solo archivos involucrados; localiza con `glob`/`grep` antes de `read`.
- Carga `references/*` solo si la tarea lo requiere (ver INDEX).
- Referencia `path:línea`, no pegues bloques grandes.
- No reanalices el proyecto sin motivo.

## Flujo obligatorio
1. Requerimientos mínimos.
2. Inspeccionar solo archivos involucrados.
3. Implementar cambios acotados.
4. Pruebas unitarias (obligatorio).
5. Verificar servicios.
6. Verificar persistencia BD ↔ sistema.
7. `flutter analyze` + `dart format .` + `flutter test`.

No cerrar tarea sin pruebas verdes.

## Responsabilidades por capa
- Models: datos. Repositories: datos/SQL. Services: lógica. Screens: UI. Widgets: reutilizables. Core: compartido.

## Persistencia SQLite
- `DatabaseHelper` único; CRUD; consultas parametrizadas; migraciones; transacciones; errores manejados.
- Ver `references/persistence/persistence-verification.md`.

## Servicios
- Sin UI; inyectables; errores tipados; tests con mocks.
- Ver `references/services/services-verification.md`.

## Estado
- `setState` (local), `Provider`, `Riverpod`, `Bloc/Cubit` según necesidad; justificar dependencias.

## Seguridad/calidad
- Sin secretos en texto plano; validar datos; SQL parametrizado; no eliminar sin autorización.

## Referencias (on-demand)
Ver `references/INDEX.md`. Carga solo el archivo relevante.
