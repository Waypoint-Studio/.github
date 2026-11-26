# Contribuir

## Flujo

1. Crear rama desde `main`: `feat/<descripcion>`, `fix/<descripcion>` o `chore/<descripcion>`.
2. Commits con [Conventional Commits](https://www.conventionalcommits.org/es/).
3. Abrir PR hacia `main` con la plantilla completa.
4. El PR se integra con CI en verde y la revisión aprobada, usando *squash merge*.

## Estándares

- TypeScript estricto, pnpm como gestor de paquetes.
- Imports con alias `@/`, sin rutas relativas `../`.
- Funciones flecha para funciones sueltas.
- Reglas de SonarQube sin issues nuevos.
- Logs mínimos: solo `error` y `warn` en producción.
