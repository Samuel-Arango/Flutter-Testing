# Plan de testeo

Objetivo: definir qué, cómo y cuándo probar.

## Niveles

- **Unitarias**: models, repos, services, utils.
- **Widgets**: componentes UI críticos.
- **Integración**: flujos clave (navegación, persistencia).

## Alcance mínimo

- Models: serialización, validaciones, equality.
- Repositories: CRUD contra BD en memoria, migraciones.
- Services: lógica con dependencias mockeadas (éxito, error, inválido, vacío).
- UI: estados de carga/error/vacío y validaciones de formularios.

## Convenciones

- Un archivo de test por archivo de código: `foo_test.dart`.
- `group`/`test`; nombres descriptivos consistentes.
- Mocks con `mocktail` (preferido) o `mockito`.
- BD en memoria con `sqflite_common_ffi` (`sqfliteFfiInit`, `databaseFactoryFfi`).
- No tocar BD real en tests.

## Checklist de cierre

- [ ] `flutter analyze` sin issues.
- [ ] `dart format .` aplicado.
- [ ] `flutter test` verde.
- [ ] Cobertura de lógica nueva ≥ 80%.
- [ ] Casos de error probados.
