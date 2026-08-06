# Superpowers Governance

Strictly enforce the following instructions when creating or modifying files using `Superpowers` skills.

## Storage & Directory
- **Base Path**: All spec and plan files **MUST** be stored in the `@docs/tickets/` directory, relative to the project root.
- **Directory Creation**: Before writing any file, ensure the `@docs/tickets/` directory exists. Create it if it is missing.

## Naming Convention
When creating a new spec or plan file, **MUST** strictly adhere to the naming format: `<id>-<slug>.<type>.md`, where:
- **`<id>`** - A unique numeric or alphanumeric identifier representing the ticket (e.g., `001`, `JIRA-42`, `PROJ-123`). The same `<id>` **MUST** be used consistently across both the spec and plan files for the same ticket.
- **`<slug>`** - A short, descriptive, kebab-case text summarizing the ticket (e.g., `oauth-workflow`, `fix-login-timeout`, `add-payment-webhook`).
- **`<type>`** – **MUST** be either `spec` or `plan` (exactly).
  - Use `spec` for design spec (e.g., `001-oauth-workflow.spec.md`).
  - Use `plan` for implementation plan (e.g., `001-oauth-workflow.plan.md`).

## Governance & Enforcement
- **Single Source of Truth**: For any given ticket `<id>`, there must be exactly **one** active `spec` and exactly **one** active `plan` file. Updates must overwrite the existing files using the exact same naming format—do not create versioned copies (e.g., `v2`, `final`) unless explicitly required.
- **Mandatory Pairing**: A `plan` file **MUST NOT** be created without a corresponding `spec` file present for the same `<id>`, and vice versa (unless the skill specifically dictates otherwise).
- **Validation**: Before finalizing a new file, validate that the `<slug>` contains only lowercase letters, numbers, and hyphens (`-`), with no spaces or special characters.
