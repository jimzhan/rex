## Git & Git Workflow

- **Branching**: `main` is always deployable. Use `feature/xxx` branches for new work.
- **Commits**: Conventional Commits (`feat:`, `fix:`, `chore:`, etc.).
- **PRs**: Require at least one approval. CI must pass (lint, test, build).
- **Releases**: Tagged releases trigger automatic deployment (GitHub Actions).
