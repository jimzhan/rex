# Testing Strategy & Quality Gates

Defines the mandatory testing pyramid and coverage requirements.

## 1. Test Pyramid Definition
- **Unit (90%):** Fast, isolated tests (no DB, no Network). Focus on business logic and pure functions.
- **Integration (80%):** Tests involving database, file system, or external services (mocked or test containers).
- **E2E (20%):** End-to-end tests simulating real user journeys (requires Staging environment).

## 2. Specification Rules
- **Naming:** Test files must be named `*.spec.ts` or `*.test.ts`.
- **AAA Pattern:** Arrange, Act, Assert.
- **Mocks:** Mock external APIs; never mock internal interfaces (use test doubles only for boundaries).
- **Clean-up:** Database state must be cleaned after each integration test (use transactions or truncation).

## 3. Coverage Thresholds
- **Global Coverage:** Minimum **80%** Line/Branch/Function/Statement coverage.
- **Critical Path:** Core business logic (Domain Layer) must have **90%** coverage.
- **Red Alert:** Pull Requests that decrease overall coverage by 1% or more are **blocked**.
