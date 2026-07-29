# Technology Stack 

This is a production‑grade full‑stack TypeScript application, managed with **pnpm** workspaces.

- **Runtime** Node.js (LTS)
- **Language** TypeScript (strict mode)
- **Backend** Hono
- **Frontend** React + Vite
- **ORM** Drizzle
- **Database** PostgreSQL
- **Caching** Redis
- **Package Manager** pnpm
- **Container** Podman
- **Infrastructure** Terraform
- **Testing** Vitest (Unit), Playwrite (E2E)
- **Linting** Biome


## Project Structure

```
<project-root>/
├── packages/
│   ├── api/                        # Backend (Hono)
│   │   ├── src/
│   │   │   ├── index.ts            # App entry (Hono server)
│   │   │   ├── app.ts              # Hono app instance, middleware, routes
│   │   │   ├── routes/             # Route handlers (controllers)
│   │   │   │   ├── health.ts
│   │   │   │   ├── auth.ts
│   │   │   │   └── users.ts
│   │   │   ├── services/           # Business logic (use cases)
│   │   │   │   ├── auth.service.ts
│   │   │   │   └── user.service.ts
│   │   │   ├── repositories/       # Data access layer (Drizzle queries)
│   │   │   │   ├── user.repo.ts
│   │   │   │   └── session.repo.ts
│   │   │   ├── middleware/         # Custom Hono middleware
│   │   │   │   ├── auth.ts
│   │   │   │   └── logger.ts
│   │   │   ├── schemas/            # Zod validation schemas (shared with frontend?)
│   │   │   │   └── user.schema.ts
│   │   │   ├── utils/              # Helpers (JWT, hashing, etc.)
│   │   │   └── types/              # Internal TypeScript types
│   │   ├── test/
│   │   │   ├── unit/               # Vitest unit tests
│   │   │   └── integration/        # API integration tests (Vitest)
│   │   ├── drizzle/                # Drizzle migrations & schema
│   │   │   ├── schema/             # Drizzle table definitions
│   │   │   │   ├── users.ts
│   │   │   │   └── sessions.ts
│   │   │   ├── migrations/         # Auto‑generated migration files
│   │   │   └── drizzle.config.ts   # Drizzle config
│   │   ├── package.json
│   │   ├── tsconfig.json           # Extends root tsconfig
│   │   ├── vitest.config.ts        # Unit/integration test config
│   │   └── .env.example            # API‑specific env vars
│   │
│   ├── web/                        # Frontend (React + Vite)
│   │   ├── src/
│   │   │   ├── main.tsx            # React entry
│   │   │   ├── App.tsx
│   │   │   ├── features/           # Feature‑based modules
│   │   │   │   ├── auth/
│   │   │   │   │   ├── components/
│   │   │   │   │   ├── hooks/
│   │   │   │   │   └── api/        # API calls to backend
│   │   │   │   └── dashboard/
│   │   │   ├── shared/             # Shared UI, utilities, types
│   │   │   │   ├── ui/             # Reusable components (Button, Card, etc.)
│   │   │   │   ├── lib/            # Helpers, fetchers, formatters
│   │   │   │   └── types/          # Shared TS types (can re‑export from @myapp/shared)
│   │   │   ├── hooks/              # Global custom hooks
│   │   │   ├── context/            # React Context providers
│   │   │   └── routes/             # Route definitions (React Router)
│   │   ├── test/
│   │   │   └── e2e/                # Playwright E2E tests
│   │   │       └── auth.spec.ts
│   │   ├── index.html
│   │   ├── package.json
│   │   ├── tsconfig.json
│   │   ├── vite.config.ts
│   │   ├── playwright.config.ts    # Playwright config
│   │   └── .env.example
│   │
│   ├── shared/                     # Shared code between api and web
│   │   ├── src/
│   │   │   ├── types/              # Shared TypeScript interfaces, enums
│   │   │   │   ├── user.ts
│   │   │   │   └── api.ts
│   │   │   ├── constants/          # App‑wide constants
│   │   │   ├── utils/              # Pure helpers (date formatting, etc.)
│   │   │   └── validators/         # Zod schemas reused by both frontend & backend
│   │   ├── package.json
│   │   └── tsconfig.json
│   │
│   └── db/                         # (Optional) DB‑only package for migrations/seeding
│       ├── src/
│       │   ├── seed.ts
│       │   └── client.ts           # Drizzle client (re‑exported for api)
│       ├── drizzle/                # Symlink or copy from api/drizzle
│       ├── package.json
│       └── tsconfig.json
│
├── infra/                          # Infrastructure as Code (Terraform)
│   ├── environments/
│   │   ├── dev/
│   │   │   ├── main.tf
│   │   │   ├── variables.tf
│   │   │   └── terraform.tfvars
│   │   ├── staging/
│   │   └── prod/
│   ├── modules/                    # Reusable Terraform modules
│   │   ├── network/
│   │   ├── db/
│   │   └── app/
│   └── global/                     # Shared resources (e.g., IAM, VPC)
│
├── docker/                         # Podman/Docker build files
│   ├── api.Dockerfile
│   ├── web.Dockerfile              # Optional static build (or served via S3)
│   ├── db.Dockerfile               # Postgres with init scripts (optional)
│   └── redis.Dockerfile            # Redis config (optional)
│
├── scripts/                        # Utility scripts
│   ├── dev-up.sh                   # Start all services locally (Podman Compose)
│   └── migrate.sh                  # Run Drizzle migrations
│
├── tests/                          # Global E2E (Playwright) – can also live in packages/web
│   └── global-setup.ts             # Setup for E2E (e.g., test database)
│
├── .github/                        # CI/CD workflows
│   └── workflows/
│       ├── ci.yml
│       └── deploy.yml
│
├── .biome.json                     # Biome configuration (Lint + Format)
├── .env.example                    # Root env (shared vars, e.g., DATABASE_URL)
├── .gitignore
├── .npmrc                          # pnpm settings (strict‑peer‑deps, etc.)
├── package.json                    # Root package.json (private workspaces)
├── pnpm-workspace.yaml             # Workspace definition
├── tsconfig.base.json              # Shared TypeScript base configuration
├── tsconfig.json                   # Root tsconfig (references workspaces)
├── vitest.workspace.ts             # Vitest workspace config (runs all packages)
├── docker-compose.yml              # Podman‑compatible compose for local dev
├── terraform.tf                    # (optional) root Terraform wrapper
└── README.md
```
