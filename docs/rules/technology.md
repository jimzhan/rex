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
- **Infrastructure** Terraform
- **Testing** Vitest (Unit), Playwrite (E2E)
- **Linting** Biome


## Project Structure

```
my-app/
├── packages/
│   ├── api/                        # Backend (Hono)
│   │   ├── src/
│   │   │   ├── routes/             # Route handlers (grouped by domain)
│   │   │   │   ├── health.ts
│   │   │   │   ├── auth.ts
│   │   │   │   └── users.ts
│   │   │   ├── services/           # Business logic (domain services)
│   │   │   │   ├── auth.service.ts
│   │   │   │   └── user.service.ts
│   │   │   ├── repositories/       # Data access layer (Drizzle queries)
│   │   │   │   ├── user.repo.ts
│   │   │   │   └── session.repo.ts
│   │   │   ├── middleware/         # Hono middleware (auth, logging, etc.)
│   │   │   │   ├── auth.ts
│   │   │   │   └── logger.ts
│   │   │   ├── validators/         # Zod schemas (request/response validation)
│   │   │   │   ├── auth.schema.ts
│   │   │   │   └── user.schema.ts
│   │   │   ├── lib/                # Shared utilities (Redis client, config, etc.)
│   │   │   │   ├── redis.ts
│   │   │   │   └── config.ts
│   │   │   ├── types/              # Internal types (not shared with frontend)
│   │   │   │   └── custom.d.ts
│   │   │   └── index.ts            # App entry (Hono app export)
│   │   ├── tests/
│   │   │   ├── unit/               # Vitest unit tests
│   │   │   └── integration/        # API integration tests
│   │   ├── drizzle/                # Drizzle migrations & schema
│   │   │   ├── schema/             # Table definitions
│   │   │   │   ├── users.ts
│   │   │   │   └── sessions.ts
│   │   │   ├── migrations/         # Auto-generated migration files
│   │   │   └── drizzle.config.ts
│   │   ├── package.json
│   │   ├── tsconfig.json
│   │   ├── vitest.config.ts
│   │   └── .env.example
│   │
│   ├── web/                        # Frontend (React + Vite)
│   │   ├── src/
│   │   │   ├── features/           # Feature‑based modules
│   │   │   │   ├── auth/
│   │   │   │   │   ├── components/
│   │   │   │   │   ├── hooks/
│   │   │   │   │   └── services/
│   │   │   │   └── dashboard/
│   │   │   ├── shared/             # Cross‑cutting code
│   │   │   │   ├── ui/             # Reusable presentational components
│   │   │   │   ├── lib/            # Utilities (API client, formatters)
│   │   │   │   └── types/          # Shared frontend types
│   │   │   ├── pages/              # Route‑level pages (React Router)
│   │   │   ├── App.tsx
│   │   │   └── main.tsx
│   │   ├── tests/
│   │   │   └── e2e/                # Playwright E2E tests
│   │   ├── index.html
│   │   ├── package.json
│   │   ├── tsconfig.json
│   │   ├── vite.config.ts
│   │   └── playwright.config.ts
│   │
│   └── shared/                     # Shared code (types, constants, utilities)
│       ├── src/
│       │   ├── types/              # Shared TypeScript interfaces/types
│       │   │   ├── user.ts
│       │   │   └── api.ts
│       │   ├── constants/          # App‑wide constants (status codes, etc.)
│       │   └── utils/              # Pure utility functions
│       ├── package.json
│       └── tsconfig.json
│
├── infra/                          # Terraform infrastructure (IaC)
│   ├── environments/
│   │   ├── dev/
│   │   │   ├── main.tf
│   │   │   ├── variables.tf
│   │   │   └── terraform.tfvars
│   │   ├── staging/
│   │   └── production/
│   ├── modules/                    # Reusable Terraform modules
│   │   ├── networking/
│   │   ├── database/
│   │   └── compute/
│   └── shared/                     # Shared Terraform configs (backend, providers)
│
├── docker-compose.yml              # Local services (PostgreSQL, Redis)
├── package.json                    # Root package.json (workspace definition)
├── pnpm-workspace.yaml             # pnpm workspaces config
├── tsconfig.json                   # Base TypeScript config (inherited by packages)
├── biome.json                      # Biome configuration (lint + format)
├── .env.example                    # Root environment variables template
├── .gitignore
├── .pre-commit-config.yaml         # Optional: pre‑commit hooks
├── README.md
└── AGENTS.md                       # Your AI‑agent instructions
```
