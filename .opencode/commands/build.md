---
name: build
description: "Implement against the execution plan in an isolated Git worktree."
---

# Build

Implement against the execution plan in an isolated Git worktree.

## Ground Rules

- **MUST** verify the requirement is provided before proceeding. If missing, ask the user for it.
- **DO NOT** invoke `/writing-plans` to create an implementation plan.
- **Ticket ID & Slug Generation**:
  - If the source is a URL (e.g., Jira, Linear, GitHub), attempt to extract the ticket ID (e.g., `PROJ-123`, `XXX-12`, `GH-456`).
  - If no ID can be extracted (e.g., free text or local file), scan the existing `docs/specs/` directory and generate a zero-padded three‑digit sequential number starting from `001` (e.g., `001`, `002`).
  - Generate the `slug` by taking the key of the requirement and converting it to kebab-case (e.g., `add-oauth-flow`).
- **MUST** use `docs/specs/<ticket-id>-<slug>.md` for all new spec files.

## The Process

### Step 1: **Start implementation**:
  - **Prerequisite Check:** Before initiating this step, **MUST** verify:
    - **Step 3** has successfully generated the execution plan inside the worktree **and** the user has explicitly approved that plan.
    - Ensure you are operating within the isolated worktree directory
  - Run `/subagent-driven-development` to execute the approved plan task by task, committing progress incrementally.
  - Monitor the subagent's output and handle any intermediate failures according to its own error-handling rules. If the subagent cannot proceed, halt and report to the user.

