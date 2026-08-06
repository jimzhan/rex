---
name: think
description: "Analyze an idea from <Ticket URL | Local file | Free text>, convert it into a technical design spec and WBS in an isolated Git worktree."
argument-hint: "<ticket-url | local-file-path | free-text>"
---
# Think

Think through your idea and turn it into a technical design specification and a detailed WBS for execution.

## Ground Rules

- **MUST** verify the requirement is provided before proceeding. If missing, ask the user for it.
- **Convention**
  - **MUST** use `@docs/tickets/` as the ***root** for all new artifacts.
  - **MUST** use `<id>-<slug>.<spec | plan>.md` under the ***root*** for all new spec and plan files.
  - **MUST** extract ticket ID from the given source, if missing, generate a zero-padded 3‑digit sequential number starting from `001` (e.g., `001`, `002`).
  - **MUST** generate the `slug` by taking the key of the requirement and converting it to kebab-case (e.g., `oauth-flow`).
  - **MUST** use `<id>-<slug>` for the Git worktree directory and branch name.
- **DO NOT** invoke `/subagent-driven-development` or `/executing-plans` for implementation.

## Process

**Critical Rule:** Execute the following steps in **strict sequential order**. **DO NOT** proceed to the next step until the current step's **AC** are fully met. If any step fails irrecoverably, halt immediately and report the failure to the user with a clear explanation.

### Step 1: Create an isolated workspace for ideation
- Run `/using-git-worktrees` to create a dedicated Git worktree.
- Verify that the worktree is successfully created: the directory exists, and the new branch is checked out.
- Once verified, switch your shell context into the new worktree directory.
- **AC** Confirm the new Git worktree is ready and is the current working directory. If creation fails, halt and report the error.

### Step 2: Convert the requirement into technical design sepc
- Run `/brainstorming` to deeply analyze the user's requirement, clarify ambiguities, and surface potential risks, edge cases, and dependencies.
- Present a concise summary of the generated spec to the user (e.g., the file path and a brief outline).
- Explicitly request the user to provide **explicit written approval** (e.g., "Approved", "Proceed", or similar affirmative response).
- **AC** The spec exists inside the new worktree and the user has typed an explicit approval phrase after the spec summary was presented.

### Step 3: Create a detailed WBS for execution
- Run `/writing-plans` to generate a detailed, actionable execution plan **inside the newly created Git worktree**.
- Present a concise summary of the plan for final review.
- **AC** The plan file exists inside the worktree and a summary has been presented to the user.

---

**Next Step:** Once the artifacts are approved, inform the user that the isolated workspace is ready. The next command is `/build`, but **do not** run it automatically.
