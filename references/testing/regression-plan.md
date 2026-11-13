# Plan de regresión

Objetivo: asegurar que cambios no rompen funcionalidad existente.

## Estrategia

1. Ejecutar suite completa de tests antes y después del cambio.
2. Identificar tests afectados por los archivos modificados.
3. Añadir tests para bugs corregidos (no regresión).
4. Probar flujos críticos manualmente (smoke test).
5. Verificar persistencia/migraciones si hubo cambios de BD.

## Checklist

- [ ] Tests existentes pasan antes del cambio.
- [ ] Tests existentes pasan después del cambio.
- [ ] Nuevos tests cubren el cambio.
- [ ] Flujos críticos (login, navegación, CRUD) verificados.
- [ ] Migración de BD probada si aplica.
- [ ] Sin warnings nuevos en `flutter analyze`.
