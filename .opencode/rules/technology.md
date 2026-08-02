# Technology Stack 

Enforce the following technology stack for implementation **unless** `@docs/rules/technology.md` is present (in which case, use `@docs/rules/technology.md` instead).

- **Auth Strategy**: Session-based with Redis (session store)
- **Runtime**: Node.js v24 (LTS)
- **Language**: TypeScript (strict mode)
- **Internationalization**: `i18next`
- **Build Tool**: `Vite`
- **Backend**
  - **Framework**: `Hono`
  - **ORM**: `Drizzle`
  - **Testing**: `Vitest` (Unit & Integration)
  - **Validation**: `Zod`
  - **Configuration** `config`
  - **API Documentation**: `@hono/zod-openapi`
  - **Authentication**: `better-auth`
  - **Logging**: `Pino`
- **Caching**: `Redis`
- **Database**: `PostgreSQL` — all tables **MUST** use UUID v7 as the primary key.
- **Frontend**
  - **Framework**: `React` + `React Router`
  - **CSS Framework**: `TailwindCSS`
  - **State Management**: `Zustand`
  - **Testing**: `Vitest` (Unit), `Playwright` (E2E)
  - **Linting & Formatting**: `@biomejs/biome`
- **IaC**: `Terraform`
- **Container**: `Podman`
- **Package Manager**: `pnpm`
- **Monorepo**: `Turborepo`
- **Folder Structure**: Follow Turborepo's recommended [folder structure](https://turborepo.dev/docs/crafting-your-repository/structuring-a-repository#declaring-directories-for-packages) (apps/ for applications, packages/ for libraries and tooling).
