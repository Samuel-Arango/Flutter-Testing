# Verificación de persistencia (BD ↔ sistema)

Objetivo: garantizar integridad entre la capa de datos y el sistema.

## Elección de solución

- `sqflite`: SQL local, migraciones, relaciones → usar para datos estructurados/relacionales.
- `drift`: tipado, queries complejas, streams → preferir cuando el esquema crece o se necesitan streams.
- `shared_preferences`: pares clave-valor simples (flags, settings).
- `flutter_secure_storage`: secretos/tokens (nunca en texto plano ni en prefs).

## Implementación (SQLite)

- `DatabaseHelper` único; apertura/creación versionada.
- Tablas y relaciones bien definidas.
- CRUD completo; consultas parametrizadas.
- Transacciones para operaciones múltiples.
- Migraciones incrementales con `onUpgrade`; no borrar datos sin justificación.
- Repositorios encapsulan todo SQL; pantallas no ejecutan SQL.
- Modelos con `toMap`/`fromMap` y mapeo explícito.
- Manejo de errores; excepciones tipadas.

## Verificación obligatoria

1. Round-trip: insertar → leer → comparar objeto completo.
2. Update y delete reflejados en lecturas posteriores.
3. Consultas filtradas (where) devuelven subconjuntos correctos.
4. Migración: BD v(n-1) → v(n) conserva datos y crea nuevas columnas/tablas.
5. Integridad referencial: FKs y cascadas funcionan.
6. Concurrencia: operaciones simultáneas no corrompen datos (transacciones).
7. Errores: constraint violations se propagan como excepciones tipadas.

## Tests (BD en memoria)

- Usar `sqflite_common_ffi` con `databaseFactoryFfi`.
- `sqfliteFfiInit()` en `setUpAll`; cerrar BD en `tearDown`.
- No tocar BD real en tests.

## Checklist

- [ ] Solución elegida justificada.
- [ ] Round-trip insert/read verificado.
- [ ] Update/delete verificados.
- [ ] Migración probada.
- [ ] FKs/cascadas probadas.
- [ ] Errores de constraint probados.
- [ ] BD en memoria en tests.
