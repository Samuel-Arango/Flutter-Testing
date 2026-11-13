# Seguridad y calidad

Objetivo: código seguro y de calidad.

## Seguridad

- No almacenar contraseñas en texto plano.
- No exponer credenciales ni claves privadas.
- Validar datos antes de almacenarlos.
- Evitar SQL vulnerable (consultas parametrizadas).
- No eliminar información del usuario sin autorización.
- Respetar privacidad de los datos.

## Calidad

- Manejar excepciones correctamente.
- `flutter analyze` sin issues.
- `dart format .` aplicado.
- Pruebas unitarias obligatorias.
- Sin código muerto ni duplicación innecesaria.

## Checklist

- [ ] Sin secretos en código.
- [ ] Validaciones presentes.
- [ ] SQL parametrizado.
- [ ] Analyze limpio.
- [ ] Tests verdes.
