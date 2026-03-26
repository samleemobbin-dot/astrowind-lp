# AGENTS.md

## Cursor Cloud specific instructions

### Project overview

AstroWind is a static website template built with **Astro 5.x** and **Tailwind CSS**. It uses `npm` as the package manager (lockfile: `package-lock.json`). Node.js >= 18.17.1 is required (see `engines` in `package.json`).

### Key commands

All standard commands are documented in `README.md` under "Commands". Key ones:

- `npm run dev` — starts dev server on `localhost:4321` (add `-- --host 0.0.0.0` for network access)
- `npm run build` — production build to `./dist/`
- `npm run check` — runs `astro check`, ESLint, and Prettier checks
- `npm run check:eslint` — ESLint only
- `npm run fix` — auto-fix ESLint and Prettier issues

### Non-obvious caveats

- **Project structure**: Source files live in `src/` (components, pages, layouts, utils, data, content, config). The `astro.config.ts` and all imports use the `~/` path alias which maps to `src/` (configured in `tsconfig.json`).
- **Missing `src/` on main branch**: The original `main` branch had source files at the repo root instead of `src/`, and was missing critical utility files (`src/utils/*`, `src/config.yaml`, `src/navigation.ts`, blog pages). These were added as part of environment setup. If you encounter import errors referencing `~/utils/*` or `./src/utils/frontmatter`, ensure the `src/` directory structure exists.
- **Virtual module `astrowind:config`**: Site configuration is loaded from `src/config.yaml` via a custom Astro integration in `vendor/integration/`. The integration creates a virtual module `astrowind:config` that exports `SITE`, `METADATA`, `APP_BLOG`, `UI`, `ANALYTICS`, `I18N`.
- **Content collections**: Blog posts live in `src/data/post/` (not `src/content/post/`). The content config is at `src/content/config.ts`.
- **Prettier warnings**: Running `npm run check:prettier` will report formatting differences. This is expected given the existing code style. Use `npm run fix` to auto-format if needed.
- **No automated test suite**: This project does not have unit/integration tests. Verification is done via `npm run check` (type checking + linting) and `npm run build` (full static build).
