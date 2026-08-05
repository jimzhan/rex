---
name: plan
description: Create a detailed WBS for execution plan before implementation.
---

# Plan

Plan with the newly created technical design spec.

## Ground Rules

- **DO NOT** proceed with the **Execution Handoff**.
- **MUST** switch into the same worktree directory as the spec for plans.
- **MUST** use `docs/plans/<ticket-id>-<slug>.md` for all new plan files.

## The Process

### Step 1: Create detailed WBS
  - Run `/writing-plans` to generate a detailed, actionable execution plan.
  - **Output Artifact:** Write the final execution plan **inside the newly created Git worktree**.
  - **AC** Wait for the user to provide explicit written approval of the execution plan. **DO NOT** move to Step 4 until this approval is received.

---

**Next Step:** Once the plan is approved, inform the user. **DO NOT** run `/build` automatically - wait for the user to explicitly invoke it. The next command is `/build`.
