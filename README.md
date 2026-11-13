# Flutter-agent-skill

Skill técnica para agentes de código especializada en desarrollo de aplicaciones móviles con **Flutter** y **Dart**. Define un conjunto de reglas, flujos y referencias verificables para producir código de calidad con consumo mínimo de contexto.

---

## 1. ¿De qué trata la skill?

`flutter-development` es un **paquete de instrucciones estructuradas** (skill) que un agente de código carga cuando la tarea involucra Flutter/Dart. No es código ejecutable: es conocimiento operativo codificado en Markdown que guía al agente en:

- Análisis de proyectos Flutter existentes.
- Diseño e implementación de UI, estado y navegación.
- Persistencia local con SQLite (`sqflite`).
- Arquitectura modular (Models, Repositories, Services, Screens, Widgets, Core).
- Pruebas unitarias, de widgets e integración.
- Verificación de servicios y persistencia BD ↔ sistema.
- Depuración, seguridad y calidad.

La skill se activa por coincidencia de su `description` con la tarea del usuario y se inyecta en el contexto del agente.

---

## 2. ¿Por qué se crea?

### Problemas que resuelve

1. **Sobrecarga de contexto**: cargar toda la documentación de Flutter en cada tarea consume tokens innecesarios y degrada la precisión. La skill se divide en un archivo principal lean + referencias on-demand.
2. **Falta de verificación**: implementaciones sin pruebas ni verificación de persistencia/servicios generan regresiones. La skill impone pruebas unitarias obligatorias y checklists de verificación.
3. **Inconsistencia arquitectónica**: sin guía, el agente puede mezclar SQL en pantallas, instanciar repositorios dentro de servicios, etc. La skill define responsabilidades por capa.
4. **No determinismo**: distintas ejecuciones producían resultados distintos. La skill estandariza flujo, convenciones y comandos (`flutter analyze`, `dart format .`, `flutter test`).

### Objetivos de diseño

- **Lean**: `SKILL.md` < ~80 líneas; detalles en `references/*`.
- **On-demand**: las referencias se cargan solo cuando la tarea lo requiere.
- **Verificable**: cada cambio debe pasar analyze/format/test y checklists.
- **Trazable**: plan de requerimientos, análisis, testeo y regresión documentados.
- **Modular**: referencias independientes por área (contexto, persistencia, servicios, etc.).

---

## 3. Formato de una skill (opencode)

Una skill es un directorio con al menos `SKILL.md`:

```
<skill-name>/
├── SKILL.md          # Obligatorio: frontmatter + instrucciones
└── references/       # Opcional: documentos de apoyo
```

### Frontmatter de `SKILL.md`

```yaml
---
name: flutter-development
description: Especialista Flutter/Dart. Usar para UI, estado, navegación, SQLite, arquitectura, depuración y pruebas. Prioriza contexto mínimo, pruebas unitarias obligatorias, verificación de servicios y persistencia BD.
---
```

- `name`: identificador único de la skill.
- `description`: texto usado por el agente para decidir si activar la skill. Debe ser conciso y cubrir los casos de uso.

El cuerpo de `SKILL.md` son instrucciones en Markdown que se inyectan en el contexto del agente al activarse.

---

## 4. Estructura del repositorio

```
Flutter-agent-skill/
├── SKILL.md                          # Skill principal (lean)
├── README.md                         # Este documento
├── LICENSE
└── references/
    ├── INDEX.md                      # Índice de referencias (on-demand)
    ├── context/
    │   └── context-minimum.md        # Reglas de contexto mínimo
    ├── requirements/
    │   ├── requirements-analysis.md  # Análisis de requerimientos
    │   └── requirements-plan.md     # Plan de requerimientos trazable
    ├── testing/
    │   ├── test-plan.md              # Plan de testeo
    │   └── regression-plan.md        # Plan de regresión
    ├── framework/
    │   └── flutter-usage.md          # Uso del framework Flutter/Dart
    ├── persistence/
    │   └── persistence-verification.md  # Verificación persistencia BD
    ├── services/
    │   └── services-verification.md  # Verificación de servicios
    ├── architecture/
    │   └── architecture-plan.md      # Plan de arquitectura modular
    └── quality/
        └── security-quality.md      # Seguridad y calidad
```

### Responsabilidad de cada archivo

| Archivo | Responsabilidad |
|---|---|
| `SKILL.md` | Instrucciones operativas mínimas + punteros a referencias. |
| `references/INDEX.md` | Mapa de referencias para carga selectiva. |
| `context/context-minimum.md` | Reglas para no sobrecargar el contexto del agente. |
| `requirements/requirements-analysis.md` | Cómo analizar requerimientos antes de codificar. |
| `requirements/requirements-plan.md` | Estructura de un plan de requerimientos verificable. |
| `testing/test-plan.md` | Niveles, alcance, convenciones y checklist de pruebas. |
| `testing/regression-plan.md` | Estrategia y checklist de regresión. |
| `framework/flutter-usage.md` | Uso correcto de Flutter/Dart (widgets, navegación, estado, rendimiento). |
| `persistence/persistence-verification.md` | Implementación y verificación de persistencia SQLite. |
| `services/services-verification.md` | Implementación y verificación de servicios. |
| `architecture/architecture-plan.md` | Estructura modular y responsabilidades por capa. |
| `quality/security-quality.md` | Seguridad y calidad del código. |

---

## 5. Contexto mínimo (estrategia de tokens)

El agente debe evitar cargar información no necesaria:

1. **Localizar antes de leer**: usar `glob`/`grep` para encontrar símbolos; luego `read` con `offset`/`limit`.
2. **Carga selectiva de referencias**: solo el archivo relevante a la tarea (ver INDEX).
3. **Referencias por línea**: citar `path:línea` en lugar de pegar bloques grandes.
4. **No reanalizar**: reutilizar contexto ya obtenido.
5. **Excluir generados**: no leer `.dart_tool/`, `build/`.

Esto reduce tokens consumidos y mejora la precisión al mantener el contexto enfocado.

---

## 6. Flujo obligatorio de desarrollo

1. Analizar requerimientos mínimos.
2. Inspeccionar solo archivos involucrados.
3. Implementar cambios acotados.
4. Escribir/actualizar pruebas unitarias (obligatorio).
5. Verificar servicios implementados.
6. Verificar persistencia BD ↔ sistema.
7. Ejecutar `flutter analyze`, `dart format .`, `flutter test`.

**No se cierra una tarea sin pruebas verdes.**

---

## 7. Arquitectura

### Estructura de proyecto recomendada

```
lib/
  core/
    constants/
    database/
    utils/
  models/
  repositories/
  services/
  screens/
  widgets/
  main.dart
```

### Responsabilidades por capa

| Capa | Responsabilidad |
|---|---|
| `models/` | Representación de datos; serialización `toMap`/`fromMap`; validaciones; equality. |
| `repositories/` | Acceso y administración de datos; encapsula todo SQL; transacciones. |
| `services/` | Operaciones y lógica especializada; sin dependencia de UI; inyectables. |
| `screens/` | Pantallas de la aplicación; no ejecutan SQL ni lógica de negocio. |
| `widgets/` | Componentes reutilizables. |
| `core/` | Configuración y recursos compartidos (BD, constantes, utils). |

Principios: SOLID y separación de responsabilidades cuando pertinentes. No introducir complejidad arquitectónica innecesaria. No reemplazar arquitectura existente sin justificación técnica.

---

## 8. Persistencia SQLite

### Implementación

- `DatabaseHelper` único gestiona apertura/creación versionada.
- Tablas y relaciones bien definidas.
- CRUD completo; consultas parametrizadas.
- Transacciones para operaciones múltiples.
- Migraciones incrementales con `onUpgrade`.
- Evitar conexiones duplicadas; encapsular SQL en repositories.
- Manejo de errores; excepciones tipadas.

### Verificación obligatoria (BD ↔ sistema)

1. Round-trip: insertar → leer → comparar objeto completo.
2. Update y delete reflejados en lecturas posteriores.
3. Consultas filtradas (`where`) devuelven subconjuntos correctos.
4. Migración: BD v(n-1) → v(n) conserva datos y crea nuevas columnas/tablas.
5. Integridad referencial: FKs y cascadas funcionan.
6. Concurrencia: operaciones simultáneas no corrompen datos.
7. Errores: constraint violations se propagan como excepciones tipadas.

### Tests

- Usar `sqflite_common_ffi` con `databaseFactoryFfi`.
- `sqfliteFfiInit()` en `setUpAll`; cerrar BD en `tearDown`.
- No tocar BD real en tests.

---

## 9. Servicios

### Implementación

- Sin dependencia de UI ni `BuildContext`.
- Dependencias inyectadas por constructor (repositorios, clientes HTTP).
- Interfaces/abstractas cuando haya múltiples implementaciones o para mockear.
- Errores tipados (excepciones propias o `Result`); no `print` en producción.
- Métodos puros cuando sea posible; side effects aislados.

### Verificación obligatoria

1. Test unitario del servicio con mocks de dependencias.
2. Casos: éxito, error de dependencia, datos inválidos, vacío.
3. Verificar que no se llame a dependencias cuando la validación falla (early return).
4. Verificar transformaciones DTO ↔ modelo.
5. Si el servicio llama a varios repos, verificar orden y transaccionalidad.

### Señales de alerta

- Servicio que instancia repositorios internamente.
- Servicio que usa `setState` o `Navigator`.
- Lógica de negocio en widgets.
- Errores tragados silenciosamente.

---

## 10. Pruebas

### Niveles

- **Unitarias**: models, repositories, services, utils.
- **Widgets**: componentes UI críticos.
- **Integración**: flujos clave (navegación, persistencia).

### Alcance mínimo

- Models: serialización, validaciones, equality.
- Repositories: CRUD contra BD en memoria, migraciones.
- Services: lógica con dependencias mockeadas (éxito, error, inválido, vacío).
- UI: estados de carga/error/vacío y validaciones de formularios.

### Convenciones

- Un archivo de test por archivo de código: `foo_test.dart`.
- `group`/`test`; nombres descriptivos consistentes.
- Mocks con `mocktail` (preferido) o `mockito`.
- BD en memoria con `sqflite_common_ffi`.
- No tocar BD real en tests.

### Checklist de cierre

- [ ] `flutter analyze` sin issues.
- [ ] `dart format .` aplicado.
- [ ] `flutter test` verde.
- [ ] Cobertura de lógica nueva ≥ 80%.
- [ ] Casos de error probados.

---

## 11. Regresión

### Estrategia

1. Ejecutar suite completa de tests antes y después del cambio.
2. Identificar tests afectados por los archivos modificados.
3. Añadir tests para bugs corregidos (no regresión).
4. Probar flujos críticos manualmente (smoke test).
5. Verificar persistencia/migraciones si hubo cambios de BD.

### Checklist

- [ ] Tests existentes pasan antes del cambio.
- [ ] Tests existentes pasan después del cambio.
- [ ] Nuevos tests cubren el cambio.
- [ ] Flujos críticos (login, navegación, CRUD) verificados.
- [ ] Migración de BD probada si aplica.
- [ ] Sin warnings nuevos en `flutter analyze`.

---

## 12. Uso del framework Flutter

- Widgets reutilizables; composición sobre duplicación.
- Separar widgets de lógica de negocio.
- `StatelessWidget`/`StatefulWidget` correctos.
- Navegación y rutas organizadas.
- Ciclos de vida correctos; evitar rebuilds innecesarios (`const`, `RepaintBoundary`, keys).
- Null safety estricto; convenciones oficiales de Dart.
- `const` constructors; `ListView.builder` para listas largas.
- Evitar trabajo pesado en `build`.
- Verificar en Android/iOS (y web/desktop si aplica).
- Respetar safe areas y tamaños de pantalla.

### Gestión de estado

Elegir según necesidad: `setState` (local), `Provider`, `Riverpod`, `Bloc/Cubit`. Justificar cada dependencia nueva.

---

## 13. Seguridad y calidad

- No almacenar contraseñas en texto plano.
- No exponer credenciales ni claves privadas.
- Validar datos antes de almacenarlos.
- Evitar SQL vulnerable (consultas parametrizadas).
- No eliminar información del usuario sin autorización.
- Respetar privacidad de los datos.
- Manejar excepciones correctamente.
- `flutter analyze` limpio; `dart format .` aplicado.
- Pruebas unitarias obligatorias.

---

## 14. Dependencias

Antes de agregar paquetes:
- Verificar si ya existe una dependencia que resuelva el problema.
- Evaluar compatibilidad con el proyecto.
- Evitar paquetes innecesarios.
- Explicar qué función cumple cada dependencia.
- Solicitar autorización antes de incorporar cambios importantes.

---

## 15. Instalación / uso

La skill es un directorio autocontenido. Para usarla en cualquier agente o herramienta compatible con el formato de skills:

1. Copiar el directorio completo (con `SKILL.md` y `references/`) a la carpeta de skills del agente/herramienta.
2. Veificar que el frontmatter de `SKILL.md` (`name`, `description`) sea reconocido por el agente.
3. La skill se activa cuando la tarea del usuario coincide con su `description`.

### Rutas de ejemplo (según herramienta)

- opencode: `~/.config/opencode/skills/flutter-development/` (o `%USERPROFILE%\.config\opencode\skills\flutter-development\` en Windows).
- Otros agentes: consultar la documentación de la herramienta para la carpeta de skills/personas.

### Uso manual

También puede usarse como documentación de referencia: leer `SKILL.md` y cargar `references/*` según la tarea, sin depender de un agente.

---

## 16. Licencia

Ver `LICENSE`.
