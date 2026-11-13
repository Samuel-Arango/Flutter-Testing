# Plan de arquitectura

Objetivo: mantener organización modular y escalable.

## Estructura

```
lib/
  core/ (constants, database, utils)
  models/
  repositories/
  services/
  screens/
  widgets/
  main.dart
```

## Responsabilidades

- Models: representación de datos.
- Repositories: acceso/administración de datos.
- Services: operaciones y lógica especializada.
- Screens: pantallas.
- Widgets: componentes reutilizables.
- Core: configuración y recursos compartidos.

## Reglas

- SOLID y separación de responsabilidades cuando pertinentes.
- No introducir complejidad arquitectónica innecesaria.
- No reemplazar arquitectura existente sin justificación técnica.
- Encapsular SQL en repositories; no en pantallas.
