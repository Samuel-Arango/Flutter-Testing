# Contexto mínimo

Objetivo: no consumir más contexto del necesario durante el desarrollo.

## Reglas operativas

- Localiza con `glob`/`grep` antes de `read` completo; lee solo secciones relevantes (`offset`/`limit`).
- No cargues `pubspec.yaml` completo si solo necesitas una dependencia: busca la línea.
- No leas toda `lib/`; identifica archivos por nombre/patrón.
- Carga `references/*` solo cuando la tarea lo requiera; no todos a la vez.
- En respuestas, referencia `path:línea` en lugar de pegar bloques grandes.
- Reutiliza contexto ya obtenido; no reanalices el proyecto sin motivo.
- Evita archivos generados (`.dart_tool`, `build/`).

## Checklist rápido

- [ ] ¿El archivo es necesario para esta tarea?
- [ ] ¿Puedo leer solo una sección?
- [ ] ¿Ya tengo este contexto de un paso anterior?
