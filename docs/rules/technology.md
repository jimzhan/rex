# Technology Overview
---
title: "Technology Stack & Development Guidelines"
description: "Comprehensive technology specification and development workflow for a modular monolith monorepo."
---

## 1. Technology Stack

- **Language:** TypeScript (strict mode)
- **Runtime:** Node.js v24 (LTS)
- **Build Tool:** `Vite`
- **Internationalization:** `i18next`
- **Backend**
  - **API Framework:** `Hono`
  - **ORM:** `Drizzle`
  - **Testing:** `Vitest` (Unit & Integration)
  - **Validation:* `Zod`
  - **Configuration:** `c12`
  - **API Documentation:** `@hono/zod-openapi`
  - **Authentication:** `better-auth`
  - **Logging:** `Pino`
- **Frontend**
  - **UI Framework:** `React` + `React Router`
  - **Styling:** `TailwindCSS`
  - **State Management:** `Zustand`
  - **Testing:** `Vitest` (Unit), `Playwright` (E2E)
  - **Linting & Formatting:** `@biomejs/biome`
- **Data Storage**
  - **Primary OLTP:** `PostgreSQL`
    - **Primary Key Standard:** All tables **MUST** use UUID v7 as the primary key.
  - **Caching:** `Redis`
- **Infrastructure** `Podman` for local containers, Kubernetes, Terraform for IaC.


## 2. Folder Structure & Modularization

- **Monorepo:** `Turborepo`.
- **Folder Structure:**
  Follow Turborepo's recommended [folder structure](https://turborepo.dev/docs/crafting-your-repository/structuring-a-repository#declaring-directories-for-packages).
  ```
  apps/
    ├── api/              # Backend application (Hono Server)
    ├── web/              # Frontend application (React)
    └── ...               # (e.g., Storybook, Admin Dashboards)
  packages/
    ├── db/               # Database schema, migrations, and Drizzle client (shared)
    ├── auth/             # Authentication logic, session management
    ├── core/             # Shared business logic and types
    ├── ui/               # Shared UI component library (React)
    ├── config/           # Configuration schemas
    ├── i18n/             # Internationalization resources
    └── ...               # (e.g., eslint-config, typescript-config)
  ```
- **Module Boundaries:** Enforce that services (e.g., `packages/db`, `packages/auth`) communicate via defined API contracts, **not** via direct database access or shared in-memory state across apps.


## 3. Coding Standards

- **Formatting:** `@biomejs/biome` - CI must fail if formatting is off.
- **Linting:** `@biomejs/biome` with strict recommended rulesets.
- **Naming Conventions:**
  - **File names:** `kebab-case.ts` (for TS/TSX), `snake_case.sql` (for migrations).
  - **Classes/Interfaces:** `PascalCase`.
  - **Functions/Variables:** `camelCase`.
- **Commenting:** Public APIs **must** have JSDoc style comments. Private logic should explain *"why"*, not *"what"*.


## 4. Git Workflow & Commit Strategy

- **Branching Strategy:** GitHub Flow (short-lived feature branches off `main`, deploy from branches, and use pull requests).
- **Commit Convention:** **Conventional Commits** (`feat:`, `fix:`, `chore:`, `perf:`, `docs:`).
- **Pull Request Requirements:**
  - Minimum 1 approving reviewer (2 for core domain changes).
  - All CI checks passing (Build, Lint, Tests, Security Scan).
  - Linear history required (Rebase merging enforced).


## 5. Database & Data Migration Strategy

- **Schema Changes:** Use `Drizzle Kit` (via `packages/db`) to generate migrations.
- **Migration Rules:**
  - Migrations must be **backward-compatible** (add columns before removing).
  - Rolling back requires a reverse migration script.
  - **Never** manually edit production DB.
- **Data Seeding:** Standardized fixtures for local and test environments using Drizzle's seeding capabilities.


## 6. Testing Strategy (The Test Pyramid)

- **Unit Tests:**
  - **Backend:** `Vitest` (>= **80%**).
  - **Frontend:** `Vitest` (Component logic).
  - Mock external dependencies.
- **Integration Tests:** `Vitest` to verify database, message queues, and 3rd-party SDKs using Podman containers.
- **Contract Tests:** Implement producer/consumer contract testing (e.g., Pact) for inter-service communication.
- **End-to-End (E2E) Tests:** `Playwright` for critical user journeys (Frontend + API).


## 7. Messaging & Event-Driven Patterns

- **Message Broker:** Kafka
- **Schema Registry:** Avro
- **Retry & Dead Letter:** Define exponential backoff strategies. Failed messages route to DLQ with alerting.
- **Idempotency:** All event consumers **must** handle duplicate messages gracefully (idempotent keys).


## 8. Logging

- **Structured Logging:** JSON format only using `Pino`. Correlation IDs (Trace IDs) injected into all logs.


## 9. Security & Secrets Management

- **Secrets:** **Never** hardcode. Use HashiCorp Vault, AWS Secrets Manager, or K8s Secrets (externally sourced).
- **Authentication & Authorization:**
  - **Auth Library:** `better-auth`.
  - **Session Store:** Redis (Session-based).
  - **Auth Strategy:** OAuth2/OIDC (e.g., Keycloak, Auth0) with Role-Based Access Control (RBAC) integrated via `better-auth`.
- **Input Validation:** Sanitize all user inputs using `Zod`. Use parameterized queries (via Drizzle) to prevent SQL injection.
- **SAST/DAST:** Run SonarQube in CI pipeline.
