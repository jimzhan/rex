---
name: spec-old
description: "Analyze an idea from <Issue URL | Local file | Free text>, convert it into a technical design spec in an isolated Git worktree."
argument-hint: "<issue-url | local-file-path | free-text>"
---

# Spec

Think through your idea and turn it into a technical design spec.

## Ground Rules

- **MUST** verify the requirement is provided before proceeding. If missing, ask the user for it.
- **DO NOT** invoke `/writing-plans` to create an implementation plan.
- **Ticket ID & Slug Generation**:
  - If the source is a URL (e.g., Jira, Linear, GitHub), attempt to extract the ticket ID (e.g., `PROJ-123`, `XXX-12`, `GH-456`).
  - If no ID can be extracted (e.g., free text or local file), scan the existing `docs/specs/` directory and generate a zero-padded three‑digit sequential number starting from `001` (e.g., `001`, `002`).
  - Generate the `slug` by taking the key of the requirement and converting it to kebab-case (e.g., `add-oauth-flow`).
- **MUST** use `docs/specs/<ticket-id>-<slug>.md` for all new spec files.

## The Process

**Critical Rule:** Execute the following steps in **strict sequential order**. **DO NOT** proceed to the next step until the current step's **AC** are fully met. If any step fails irrecoverably, halt immediately and report the failure to the user with a clear explanation.

### Step 1: Create an isolated workspace
- Run `/using-git-worktrees` to create a dedicated Git worktree.
  - **Naming convention:** Use `<ticket-id>-<slug>` for the worktree directory and branch name.
- Verify that the worktree is successfully created: the directory exists, and the new branch is checked out.
- Once verified, switch your shell context into the new worktree directory.
- **AC** Confirm the new Git worktree is ready and is the current working directory. If creation fails, halt and report the error.

### Step 2: Analyze the requirement and draft the spec
- Run `/brainstorming` to deeply analyze the user's requirement, clarify ambiguities, and surface potential risks, edge cases, and dependencies.
- **AC** The spec file exists inside the new worktree, contains a structured technical design, and is ready for review.

### Step 3: Review and obtain explicit approval
- Present a concise summary of the generated spec to the user (e.g., the file path and a brief outline).
- Explicitly request user's **written approval** to finalize the spec.
- If the user requests changes: re-run ***Step 2***.
- If the user rejects the proposal for good:
  - Halt the process gracefully.
  - Inform the user how to clean up the worktree if desired (e.g., `git worktree remove <path>`).
- **AC** The spec has been reviewed and explicitly approved by the user in writing.

---

**Next Step:** Once the spec is approved, inform the user that the isolated workspace is ready. **DO NOT** run `/plan` automatically - wait for the user to explicitly invoke it. The next command is `/plan`.
