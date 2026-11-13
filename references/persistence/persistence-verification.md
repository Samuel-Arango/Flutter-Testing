# Verificación de persistencia (BD ↔ sistema)

Objetivo: garantizar integridad entre SQLite y el sistema.

## Implementación

- `DatabaseHelper` único; apertura/creación versionada.
- Repositorios encapsulan todo SQL; pantallas no ejecutan SQL.
- Consultas parametrizadas; transacciones para operaciones múltiples.
- Migraciones incrementales con `onUpgrade`; no borrar datos sin justificación.
- Modelos con `toMap`/`fromMap` y mapeo explícito.

## Verificación obligatoria

1. Round-trip: insertar → leer → comparar objeto completo.
2. Update y delete reflejados en lecturas posteriores.
3. Consultas filtradas (where) devuelven subconjuntos correctos.
4. Migración: BD v(n-1) → v(n) conserva datos y crea nuevas columnas/tablas.
5. Integridad referencial: FKs y cascadas funcionan.
6. Concurrencia: operaciones simultáneas no corrompen datos.
7. Errores: constraint violations se propagan como excepciones tipadas.

## Tests (BD en memoria)

- Usar `sqflite_common_ffi` con `databaseFactoryFfi`.
- `sqfliteFfiInit()` en `setUpAll`; cerrar BD en `tearDown`.

## Checklist

- [ ] Round-trip insert/read verificado.
- [ ] Update/delete verificados.
- [ ] Migración probada.
- [ ] FKs/cascadas probadas.
- [ ] Errores de constraint probados.
- [ ] BD en memoria en tests.
