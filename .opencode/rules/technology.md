# Technology Stack 

- **Auth Strategy** Session-based with Redis
- **Backend**
    - **Runtime** Node.js v24 (LTS)
    - **Language** JavaScript (ES Modules)
    - **Framework** Fastify
    - **ORM** Drizzle
    - **Testing** Vitest (Unit & Integration)
- **Caching** Redis
- **Database** PostgreSQL and all tables **MUST** use UUID version 7 (time‑ordered) as the primary key
- **Frontend**
    - **Runtime** Node.js v24 (LTS)
    - **Language** TypeScript (strict mode)
    - **Framework** React + React Router
    - **Build Tool** Vite
    - **CSS Framework** TailwindCSS
    - **State Management** Zustand
    - **Testing** Vitest (Unit), Playwright (E2E)
    - **Linting & Formatting** Biome
- **IaC** Terraform
- **Container** Podman
- **Package Manager** pnpm
- **Monorepo** `Nx`
- **Folder Structure** Follow Nx recommended [folder structure](https://nx.dev/docs/concepts/decisions/folder-structure)

