# flutter-development

Skill para agentes de código especializada en desarrollo de aplicaciones móviles con **Flutter** y **Dart**.

## Propósito

Guía operativa, concisa y verificable para:
- UI, estado y navegación.
- Persistencia local (SQLite y alternativas).
- Arquitectura modular.
- Pruebas unitarias, de widgets e integración.
- Verificación de servicios y persistencia BD ↔ sistema.
- Consumo mínimo de contexto/tokens del agente.

## Estructura

```
flutter-development/
├── SKILL.md
├── README.md
├── LICENSE
├── scripts/
│   └── verify.sh
├── .github/
│   └── workflows/
│       └── verify.yml
├── evals/
│   └── prompts.md
└── references/
    ├── INDEX.md
    ├── context/
    ├── requirements/
    ├── testing/
    ├── framework/
    ├── persistence/
    ├── services/
    ├── architecture/
    └── quality/
```

## Referencias (on-demand)

Ver `references/INDEX.md`. Cada área tiene su propio documento:
- Contexto: `references/context/context-minimum.md`
- Requerimientos: `references/requirements/`
- Testeo/regresión: `references/testing/`
- Framework: `references/framework/flutter-usage.md`
- Persistencia: `references/persistence/persistence-verification.md`
- Servicios: `references/services/services-verification.md`
- Arquitectura: `references/architecture/architecture-plan.md`
- Calidad: `references/quality/security-quality.md`

## Flujo obligatorio

1. Requerimientos mínimos.
2. Inspeccionar solo archivos involucrados.
3. Implementar cambios acotados.
4. Pruebas unitarias (obligatorio, salvo cambios triviales de UI/texto).
5. Verificar servicios.
6. Verificar persistencia BD ↔ sistema.
7. `flutter analyze` + `dart format .` + `flutter test` (o `flutter test --coverage`).

Si no se pueden ejecutar las pruebas, documentar el bloqueo y el comando exacto; no afirmar "verde".

## Automatización

- `scripts/verify.sh`: corre analyze, format y test.
- `.github/workflows/verify.yml`: CI reproducible.

## Evaluación

Ver `evals/prompts.md` para prompts típicos usados para validar la skill.

## Instalación / uso

Copiar el directorio completo a la carpeta de skills del agente/herramienta. La skill se activa cuando la tarea coincide con su `description`.

## Licencia

Ver `LICENSE`.
