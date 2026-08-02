---
name: build
description: Explore user intent, convert it into a detailed execution plan, and implement it via isolated Git worktrees.
permission:
  - "*": allow
  - "rm *": ask
---

**Critical Rule:** Execute the following 4 steps in **strict sequential order**. **DO NOT** proceed to the next step until the current step's **completion criteria** are fully met. If any step fails irrecoverably, halt immediately and report the failure to the user with a clear explanation.

1. **Start exploring user intent**:
   - Run `/brainstorming` to deeply analyze the user's requirement, clarify ambiguities, and surface potential risks or edge cases.
   - **Completion Criterion:** Wait for the user to review the output and provide **explicit written approval** (e.g., "Approved", "Proceed", or similar affirmative response). **DO NOT** move to Step 2 until this approval is received.

2. **Create an isolated workspace**:
  - Run `using-git-worktrees` to create a dedicated Git worktree (Naming convention: `<YYYYMMDD>-<ticket-id>-<feature-name>` if a ticket ID is present; otherwise, use `<YYYYMMDD>-<feature-name>`.) that will isolate all planning and implementation artifacts.
  - Verify that the worktree is successfully created, the directory exists, and the new branch is checked out.
  - **Completion Criterion:** Confirm the new Git worktree is ready. **DO NOT** move to Step 3 until this finishes successfully.

3. **Create design spec and detailed execution tasks**:
   - **Prerequisite Check:** Before initiating this step, **MUST** verify:
     - **Step 1** has received explicit user approval.
     - **Step 2** has successfully created and verified the new Git worktree.
   - Once verified, switch into the new worktree directory and run `/writing-plans` to generate a detailed, actionable execution plan.
   - **Output Artifact:** Write the final execution plan **inside the newly created Git worktree** from Step 2.
   - **Completion Criterion:** Wait for the user to provide explicit written approval of the execution plan. **DO NOT** move to Step 4 until this approval is received.

4. **Start implementation**:
   - **Prerequisite Check:** Before initiating this step, **MUST** verify:
     - **Step 1** has received explicit user approval.
     - **Step 2** has successfully created and verified the new Git worktree.
     - **Step 3** has successfully generated the execution plan inside the worktree **and** the user has explicitly approved that plan.
   - Ensure you are operating within the isolated worktree directory, then run `/subagent-driven-development` to execute the approved plan task by task, committing progress incrementally.
   - Monitor the subagent's output and handle any intermediate failures according to its own error-handling rules. If the subagent cannot proceed, halt and report to the user.
