---
name: think
description: "Analyze a requirement from <Issue URL | local file | free text>, covert it into a technical design spec in an isolated Git worktree."
argument-hint: "<issue-url | local-file-path | free-text>"
---

# Think

Think through your idea and turn it into a technical design spec.

<prerequisite>
Before initiating this step, **MUST** verify the requirement is provided. If missing, ask for it.
</prerequisite>


## The Process

**Critical Rule:** Execute the following steps in **strict sequential order**. **DO NOT** proceed to the next step until the current step's **AC** are fully met. If any step fails irrecoverably, halt immediately and report the failure to the user with a clear explanation.

1. **Create an isolated workspace**:
- Use the provided ticket ID as the primary reference; if none is given, generate a zero-padded three‑digit sequential number starting from `001`.
- Run `/using-git-worktrees` to create a dedicated Git worktree (Naming convention: `<ticket-id>-<feature-name>` for artifacts.
- Verify that the worktree is successfully created, the directory exists, and the new branch is checked out.
- Once verified, switch into the new worktree directory.
- **AC** Confirm the new Git worktree is ready and is the current working directory.

2. **Start exploring user intent**:
  - Run `/brainstorming` to deeply analyze the user's requirement, clarify ambiguities, and surface potential risks or edge cases.


