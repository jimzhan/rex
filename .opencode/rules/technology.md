# Technology Stack 

- **Auth Strategy** Session-based with Redis (session store)
- **Runtime** Node.js v24 (LTS)
- **Language** TypeScript (strict mode)
- **Backend**
    - **Framework** Hono
    - **ORM** Drizzle
    - **Testing** Vitest (Unit & Integration)
    - **Validation** Zod
    - **API Documentation** @hono/zod-openapi
    - **Authentication** better-auth
    - **Logging** Pino
- **Caching** Redis
- **Database** PostgreSQL (all tables **MUST** use UUID version 7, time‑ordered, as the primary key)
- **Frontend**
    - **Framework** React + React Router
    - **Build Tool** Vite
    - **CSS Framework** TailwindCSS
    - **State Management** Zustand
    - **Testing** Vitest (Unit), Playwright (E2E)
    - **Linting & Formatting** @biomejs/biome
- **IaC** Terraform
- **Container** Podman
- **Package Manager** pnpm
- **Monorepo** `Nx`
- **Folder Structure** Follow Nx recommended [folder structure](https://nx.dev/docs/concepts/decisions/folder-structure)

