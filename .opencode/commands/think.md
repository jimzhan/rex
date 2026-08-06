---
name: think
description: "Analyze an idea from <Ticket URL | Local file | Free text>, convert it into a technical design spec and WBS in an isolated Git worktree."
argument-hint: "<ticket-url | local-file-path | free-text>"
---

# Think

Think through your idea and turn it into a technical design specification and a detailed WBS for execution.

## Ground Rules

- **MUST** verify the requirement is provided before proceeding. If missing, ask the user for it.
- **Naming Convention**
  - **MUST** extract ticket ID from the given source, if missing, generate a zero-padded three‑digit sequential number starting from `001` (e.g., `001`, `002`).
  - **MUST** generate the `slug` by taking the key of the requirement and converting it to kebab-case (e.g., `oauth-flow`).
  - **MUST** use `<id>-<slug>` for the Git worktree directory and branch name.
- **Artifacts Store**
  - **MUST** use `@docs/tickets/` as the root for all new artifacts.
  - **MUST** use `<id>-<slug>.<spec | plan>.md` under the ***root*** for all new spec or plan files.
- **DO NOT** proceed with the **Execution Handoff**.


## The Process

**Critical Rule:** Execute the following steps in **strict sequential order**. **DO NOT** proceed to the next step until the current step's **AC** are fully met. If any step fails irrecoverably, halt immediately and report the failure to the user with a clear explanation.

### Step 1: Create an isolated workspace
- Run `/using-git-worktrees` to create a dedicated Git worktree.
- Verify that the worktree is successfully created: the directory exists, and the new branch is checked out.
- Once verified, switch your shell context into the new worktree directory.
- **AC** Confirm the new Git worktree is ready and is the current working directory. If creation fails, halt and report the error.

### Step 2: Analyze the requirement and draft the spec
- Run `/brainstorming` to deeply analyze the user's requirement, clarify ambiguities, and surface potential risks, edge cases, and dependencies.
- Present a concise summary of the generated spec to the user (e.g., the file path and a brief outline).
- Explicitly request user's **written approval** to finalize the spec.
- **AC** The spec exists inside the new worktree and has been reviewed and explicitly approved by the user in writing.

### Step 3: Create a detailed WBS
  - Run `/writing-plans` to generate a detailed, actionable execution plan.
  - **Output Artifact** Write the final execution plan **inside the newly created Git worktree**.
  - **AC** Present a concise summary of all generated artifacts for user review.
