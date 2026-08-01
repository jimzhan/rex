---
name: build
description: Explore user intent, convert it into a detailed execution plan, and implement it via isolated Git worktrees.
---

**Critical Rule:** Execute the following 4 steps in **strict sequential order**. **DO NOT** proceed to the next step until the current step's **completion criteria** are fully met. If any step fails irrecoverably, halt and report the failure to the user immediately.

1. **Run `/brainstorming`**: 
- Analyze the user's requirement.
- Explore edge cases, technical trade-offs, architectural constraints, and ambiguities.
- Generate a list of critical clarifying questions for the user.
- **Completion Criterion:** Wait for the user to review the brainstorming output and provide **explicit written approval** (e.g., "Approved" or "Proceed") before moving to Step 2.

2. **Run `/using-git-worktrees`**: 
- Create a dedicated Git worktree to isolate the planning session (e.g., naming convention: `<YYYYMMDD>-<feature-name>`).
- Verify the worktree is successfully created and accessible.
- **Completion Criterion:** Confirm the new Git worktree is ready. Do not move to Step 3 until this finishes successfully.

3. **Run `/writing-plans`**: 
- **Prerequisite Check:** Before initiating this step, **MUST** verify that:
  - Step 1 has received explicit user approval.
  - Step 2 has successfully created and verified the new Git worktree.
- Once verified, execute `/writing-plans` to deeply analyze the requirement and generate a detailed, actionable execution plan.
- **Output Artifact:** Write the final execution plan **inside the newly created Git worktree** from Step 2.
- Upon completion, inform the user to review the plan.

4. **Run `implement`**
- **Prerequisite Check:** Before initiating this step, **MUST** verify that:
  - Step 1 has received explicit user approval.
  - Step 2 has successfully created and verified the new Git worktree.
  - Step 3 has successfully generated a detailed, actionable execution plan inside the worktree.
