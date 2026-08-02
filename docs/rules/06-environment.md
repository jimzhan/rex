# Environment & Configuration

Rules for managing infrastructure and application configuration.

## 1. Multi-Environment Classification
- **Local:** Developer machine.
- **Dev:** Ephemeral integration environment.
- **Testing:** Dedicated environment for automated regression suites, contract tests, and QA sign‑off.
- **Staging:** Production-parity environment. Uses anonymized production data.
- **Production:** Live traffic.

## 2. Configuration Management
- **12-Factor App:** All configuration must be stored in environment variables.
- **Hierarchy:** Environment variables override `.env` files. `.env` must never be committed to Git.
- **Validation:** Application must fail fast on startup if required environment variables are missing (validate via Zod or equivalent).

## 3. Secret & Credential Governance
- **Prohibition:** Hard-coded secrets, API keys, or passwords in source code are **strictly forbidden**.
- **Secret Manager:** Use dedicated secret vaults (e.g., AWS Secrets Manager, HashiCorp Vault, Kubernetes Secrets).
- **Rotation:** Database passwords must rotate automatically every 30 days. Application restart is required for rotation.
- **Access Control:** Developers must use personal tokens (short-lived) for access; "Root" or "Admin" privileges are locked behind an approval workflow.

