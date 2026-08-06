---
name: build
description: "Implement an approved execution plan within a dedicated Git worktree. This command assumes a prior `plan` phase produced a detailed task list. It isolates changes to avoid interfering with the main branch, verifies the plan's validity, delegates implementation to a focused subagent, and performs final checks before offering to merge."
---
# Build

Implement an approved execution plan within a dedicated Git worktree.


## Ground Rules

- **MUST** confirm the CWD is a Git worktree with the corresponding branch.
- **Convention**
  - **MUST** use `@docs/tickets/` as the ***root** for all plans.


## Process

**Critical Rule:** Execute the following steps in **strict sequential order**. **DO NOT** proceed to the next step until the current step's **AC** are fully met. If any step fails irrecoverably, halt immediately and report the failure to the user with a clear explanation.

### Step 1: Validate environment and plan
- Extract Ticket ID and Slug from current branch name.
- Search for an approved execution plan file (e.g., `<id>-<slug>.plan.md`) in the ***root***. If none exists, prompt the user to specify the correct plan.
- Present a concise summary of implementation status of the plan to the user.
- Explicitly request the user to provide **explicit written approval** (e.g., "Approved", "Proceed", or similar affirmative response).
- **AC** The plan exists inside the worktree and not full implemented, the user has typed an explicit approval phrase after the summary was presented.

### Step 2: Execute implementation via subagent
- Run `/subagent-driven-development` to execute the approved plan task by task, committing progress incrementally.
- Monitor the subagent's output in real time. If the subagent crashes or stalls, attempt a graceful restart with the same plan; if persistent, escalate to the user.
