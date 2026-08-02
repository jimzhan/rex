# Git Branching Strategy & Commit Hygiene

Standards for source control management.

## 1. Branching Strategy (Trunk-Based)
- **Main Branch (`main`):** Production-ready code. Protected. Direct commits are blocked.
- **Feature Branches:** `feature/<issue-id>-short-desc` - Branched off `main`, merged back via PR.
- **Hotfix Branches:** `hotfix/<issue-id>-short-desc` - Branched off `main`. Deployment priority.

## 2. Commit Message Conventions (Conventional Commits)
- **Format:** `<type>(<scope>): <issue-id> <subject>`
- **Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`.
- **Breaking Changes:** Must be marked with `BREAKING CHANGE:` in the body or `!` in the header (e.g., `feat(api)!: remove deprecated field`).

## 3. Code Review Rules
- **Minimum Approvals:** 2 approvals from code owners required.
- **Checklist:**
    - Logic is correct.
    - Tests are passing and written.
    - No secrets or TODOs.
    - Performance implications considered.
- **CI Check:** PRs must pass all CI pipelines (Build, Lint, Test) before merge.

## 4. Release Workflow
- **Git Tags:** Tags follow `v<major>.<minor>.<patch>`.
- **Releases:** Run the release workflow from `main`. Creates a GitHub Release and auto-updates Changelog.

