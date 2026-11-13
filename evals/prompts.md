# Evaluación de la skill (prompts típicos)

Usar estos prompts con y sin la skill para medir si mejora el resultado.

## Casos

1. "Agrega un CRUD completo con SQLite para una entidad Task (id, title, done)."
   - Esperado: DatabaseHelper, Repository, modelo toMap/fromMap, migración, tests de round-trip.
2. "Arregla este bug del widget: el botón no se deshabilita mientras carga."
   - Esperado: fix acotado, test de widget, no regresión.
3. "Implementa un servicio que sincroniza tareas con una API y persiste en SQLite."
   - Esperado: servicio sin UI, mocks, manejo de errores de red, tests.
4. "Agrega un formulario de login con validación y persistencia del token."
   - Esperado: validaciones, flutter_secure_storage para token, tests.

## Criterios de éxito

- Se generan pruebas unitarias cuando aplica.
- No se mezcla SQL en pantallas.
- Se ejecuta/propone `flutter analyze`, `dart format`, `flutter test`.
- Persistencia verificada (round-trip, migración).
- Contexto consumido razonable (no se cargan todos los references).
