# Plan de uso del framework Flutter

Objetivo: uso correcto y eficiente de Flutter/Dart.

## Estructura y widgets

- Widgets reutilizables; composición sobre duplicación.
- Separar widgets de lógica de negocio.
- `StatelessWidget`/`StatefulWidget` según estado.
- Ciclos de vida correctos; evitar rebuilds innecesarios (`const`, `RepaintBoundary`, keys).

## Navegación

- Rutas organizadas (named routes o router declarativo).
- Pasar datos por argumentos tipados, no globales.
- Manejar deep links si aplica.

## Estado

- `setState` para estado local simple.
- `Provider`/`Riverpod` para estado compartido.
- `Bloc/Cubit` para flujos complejos.
- Justificar cada dependencia nueva.

## Null safety y estilo

- Null safety estricto; evitar `!` innecesarios.
- Convenciones oficiales de Dart; `dart format .`.
- `flutter analyze` limpio.

## Rendimiento

- `const` constructors; `ListView.builder` para listas largas.
- Evitar trabajo pesado en `build`.
- Imágenes con caché y tamaños adecuados.

## Plataformas

- Verificar en Android/iOS (y web/desktop si aplica).
- Respetar safe areas y tamaños de pantalla.
