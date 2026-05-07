# Guía de Contribución

## Flujo de trabajo

1. **Fork** el repositorio
2. Crea una rama: `git checkout -b feat/mi-feature`
3. Haz tus cambios siguiendo las [Reglas de Crockford](#estándares-de-código)
4. Ejecuta `pnpm lint && pnpm test` — debe pasar sin errores
5. Abre un **Pull Request** con descripción clara

## Estándares de Código

- No `eval`, no `with`, no `++/--`
- `eqeqeq` siempre (`===`)
- `prefer-const` sobre `let` cuando sea posible
- Sin `any` en TypeScript
- Tests para toda funcionalidad nueva

## Commits

Usamos [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: añade nueva funcionalidad
fix: corrige bug
docs: actualiza documentación
chore: tarea de mantenimiento
```

## PR checklist

- [ ] Tests pasan (`pnpm test`)
- [ ] Lint pasa (`pnpm lint`)
- [ ] Documentación actualizada si aplica
- [ ] Sin secrets ni credenciales en el código
