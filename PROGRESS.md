# PROGRESS.md

Memoria del proyecto. Aquí va el estado real, lo que falta y lo que ya aprendiste.
Se actualiza al cerrar cada etapa. Si algo no está marcado, no está hecho.

**Última actualización:** 2026-10-26

---

## 1. Qué es este proyecto

Portafolio personal para mostrar quién soy, con una sección de notas/guías.
Es el campo de práctica: el objetivo **no es solo el sitio**, es aprender el stack
completo (Astro, TypeScript, Tailwind, Starlight, tests, lint, secretos, Docker,
Sentry, monorepo) antes de aplicarlo a un proyecto de empresa.

**Cómo trabajamos (reglas de la tutoría):**

1. Yo explico **qué** hay que hacer, **por qué** existe la herramienta y **cómo saber
   si funcionó**. Tú escribes los comandos y el código.
2. Un paso a la vez. Si algo falla, pegamos el error tal cual y lo leemos juntos.
3. Nada de copiar sin entender: al cerrar cada etapa me explicas con tus palabras.
4. Nada de secretos en el repo, ni ahora ni nunca.

---

## 2. Estado actual del repo

| Cosa | Estado |
|---|---|
| Node | `v22.23.4` |
| pnpm | `12.15.0` (ya instalado globalmente) |
| git | rama `main`, árbol limpio |
| Commits | ya usa conventional commits (`feat:`, `style:`) ✅ |
| Sitio | Astro 7, sin layouts ni componentes |
| Páginas | `index.astro`, `about.astro`, `blog.astro`, `posts/post-1.md` |
| Tests / lint / CI / Docker | no existen todavía |
| Estructura | monorepo pnpm: raíz (`portafolio`) + `apps/web` ✅ |
| Lockfile | `pnpm-lock.yaml` (único; npm eliminado) ✅ |

---

## 3. Glosario mínimo

Si un término no está aquí y no lo entiendes, pregúntame antes de seguir.

- **Repo (repositorio):** carpeta con historia de cambios gestionada por git.
- **Commit:** foto del estado del proyecto con un mensaje. Se puede volver atrás.
- **Rama (branch):** línea paralela de trabajo. `main` es la principal; se trabaja
  en ramas y se juntan cuando están listas.
- **Workspace:** varios paquetes en un mismo repo que comparten dependencias.
- **Monorepo:** un solo repo con varios proyectos. **No** es "varios repos".
- **Paquete:** carpeta con su propio `package.json` (aquí: `apps/web`, `apps/docs`).
- **Dependencia:** librería que el proyecto necesita (ej. `astro`).
- **Lockfile:** archivo que fija las versiones exactas instaladas (`pnpm-lock.yaml`).
  Por eso no puede haber dos lockfiles a la vez.
- **Build:** comando que convierte el código en archivos finales para publicar (`dist/`).
- **Dev server:** servidor local con recarga automática (`pnpm dev`).
- **Secret / secreto:** contraseña, token o clave. Nunca se sube al repo.

---

## 4. Estructura objetivo

```
.                       # raíz del monorepo (sin app Astro aquí)
├─ apps/
│  ├─ web/              # portafolio: landing, about, blog (Astro)
│  └─ docs/             # notas y guías (Starlight + Mermaid) — etapa 3
├─ packages/            # configuración compartida — cuando haga falta
├─ pnpm-workspace.yaml
├─ package.json         # privado, orquesta las tareas de apps/*
├─ PROGRESS.md          # este archivo
└─ turbo.json           # etapa 7
```

---

## 5. Etapas

### Etapa 0 — Base y monorepo
Objetivo: pasar de "un proyecto Astro en la raíz" a "un monorepo con el sitio dentro".
- [x] 1. Crear rama de trabajo (`chore/etapa-0-monorepo`)
- [x] 2. Borrar `node_modules`, `package-lock.json`, `.astro`
- [x] 3. Mover la app Astro a `apps/web` con `git mv` (historia conservada)
- [x] 4. Crear `pnpm-workspace.yaml` y el `package.json` de la raíz
- [x] 5. `pnpm install` (184 paquetes) y `pnpm -r build` (4 páginas)
- [x] 6. `.gitignore` con `.env.*` y excepción `!.env.example`
- [ ] 7. Commit + actualizar este archivo
- [ ] 8. Explicar con tus palabras: workspace, monorepo, lockfile, `-r` vs `--filter`

### Etapa 1 — Astro + TypeScript
- [ ] `tsconfig` estricto + `astro check`
- [ ] `Layout.astro` base y componentes reutilizables
- [ ] Content collections para el blog (schema con zod) en vez de markdown suelto
- [ ] Listado y detalle del blog generados desde la collection
- [ ] Página 404 + RSS
- [ ] Primer island (`client:*`) entendiendo cuándo **no** usar JS

### Etapa 2 — Tailwind
- [ ] Instalar Tailwind (plugin de Vite) en `apps/web`
- [ ] Definir tokens de diseño (color, tipografía, espaciado)
- [ ] Refactorizar layout y páginas
- [ ] Accesibilidad básica: contraste, foco, jerarquía de headings

### Etapa 3 — Starlight + Mermaid
- [ ] Crear `apps/docs` con Starlight
- [ ] Navegación (sidebar) y primera guía
- [ ] Mermaid con un diagrama real del proyecto
- [ ] Enlazar portafolio ↔ notas
- [ ] Decidir despliegue (subdominio vs `/docs`)

### Etapa 4 — Calidad de código
- [ ] `oxlint` (revisar errores) + script
- [ ] `oxfmt` (formatear) + script
- [ ] `knip` (código sin usar) — solo cuando haya código real
- [ ] `lefthook` (hooks de git) + `commitlint` (formato de mensajes)
- [ ] Ejercicio: provocar un commit inválido y verlo fallar

### Etapa 5 — Secretos
- [ ] `.env.example` + `.env` ignorado
- [ ] Validar variables de entorno al arrancar
- [ ] Infisical (o Bitwarden CLI) para guardar/compartir secretos
- [ ] Secretos en CI, no en `.env` de producción
- [ ] Ejercicio: simular filtración y rotar la clave

### Etapa 6 — Sentry + Docker
- [ ] Sentry con DSN por variable de entorno + source maps
- [ ] Verificar que un error de prueba llega al panel
- [ ] Medir el JS extra que añade (tensión con los "0 KB")
- [ ] `Dockerfile` multi-stage (build → servidor estático), sin secretos
- [ ] `docker compose` para probarlo en local
- [ ] Workflow de CI que construye la imagen

### Etapa 7 — turbo
- [ ] `turbo.json` con tareas (build, lint, typecheck, test)
- [ ] Cache local (y remota si interesa)
- [ ] Scripts de la raíz delegando en turbo
- [ ] Medir tiempo antes/después

---

## 6. Bitácora

| Fecha | Etapa | Aprendí | Me costó |
|---|---|---|---|
| 2026-10-26 | 0 | — | — |

---

## 7. Notas y riesgos

- Dos lockfiles = dos árboles de dependencias distintos. Uno solo.
- `astro dev` en background (`astro dev --background`), según `AGENTS.md`.
- Sentry añade JS de cliente: decidir dónde se carga.
- `turbo` no entra hasta la etapa 7: con un paquete no aporta.
- `knip` temprano da falsos positivos: se activa cuando haya código de verdad.
