# Plan de testeo

Objetivo: definir qué, cómo y cuándo probar.

## Niveles

- **Unitarias**: models, repos, services, utils.
- **Widgets**: componentes UI críticos.
- **Integración**: flujos clave (`integration_test`).
- **Golden**: snapshots de UI cuando el diseño es estable.

## Alcance mínimo

- Models: serialización, validaciones, equality.
- Repositories: CRUD contra BD en memoria, migraciones.
- Services: lógica con dependencias mockeadas (éxito, error, inválido, vacío).
- Async: `Future`/`Stream` con `expect`/`emits`; timeouts.
- HTTP: mockear cliente (mocktail) y probar status codes, parsing, errores de red.
- UI: estados de carga/error/vacío y validaciones de formularios.

## Convenciones

- Un archivo de test por archivo de código: `foo_test.dart`.
- `group`/`test`; nombres descriptivos consistentes.
- Mocks con `mocktail` (preferido) o `mockito`.
- BD en memoria con `sqflite_common_ffi` (`sqfliteFfiInit`, `databaseFactoryFfi`).
- No tocar BD real en tests.

## Cobertura

- Medir con `flutter test --coverage` (genera `coverage/lcov.info`).
- Objetivo sugerido: ≥ 80% en lógica de negocio; no exigir cobertura en UI trivial.

## Excepciones

- Cambios triviales de UI/texto no requieren pruebas unitarias nuevas, pero sí smoke test manual.
- Si el entorno no puede ejecutar tests, documentar el bloqueo y el comando exacto para el usuario; no afirmar "verde".

## Checklist de cierre

- [ ] `flutter analyze` sin issues.
- [ ] `dart format .` aplicado.
- [ ] `flutter test` verde (o bloqueo documentado).
- [ ] Cobertura medida si aplica.
- [ ] Casos de error probados.
