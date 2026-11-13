# Verificación de servicios

Objetivo: asegurar que los servicios funcionan y son testeables.

## Implementación

- Sin dependencia de UI ni `BuildContext`.
- Dependencias inyectadas por constructor.
- Interfaces/abstractas cuando haya múltiples impl o para mockear.
- Errores tipados; no `print` en producción.
- Métodos puros cuando sea posible; side effects aislados.

## Verificación obligatoria

1. Test unitario del servicio con mocks de dependencias.
2. Casos: éxito, error de dependencia, datos inválidos, vacío.
3. Verificar que no se llame a dependencias cuando la validación falla.
4. Verificar transformaciones DTO ↔ modelo.
5. Si llama a varios repos, verificar orden y transaccionalidad.

## Señales de alerta

- Servicio que instancia repositorios internamente.
- Servicio que usa `setState` o `Navigator`.
- Lógica de negocio en widgets.
- Errores tragados silenciosamente.

## Checklist

- [ ] Servicio instanciable con mocks.
- [ ] Tests de éxito y error.
- [ ] Sin dependencias de UI.
- [ ] Errores propagados/convertidos correctamente.
