<a href="#"><img alt="rex" src="https://raw.githubusercontent.com/goanywhere/rex/assets/images/rex.png" width="160px" height="64px"></a>
===

> **Status** Draft

***Rex*** is an opinionated AI-powered boilerplate designed for model-agnostic and Multi-Agent System (MAS) AI engineering. Built entirely on top of the `OpenCode` ecosystem, it provides battlefield-tested defaults to ship distributed web applications faster.

***What's included?***

- **[OpenCode](https://github.com/anomalyco/opencode)** – Model-agnostic agent orchestration.
  - **[Oh-my-opencode-slim](https://github.com/alvinunreal/oh-my-opencode-slim)** – A Multi-Agent System (MAS) for OpenCode, featuring a specialized agent team that scans codebases, fetches docs, audits architecture, builds UI, and runs scoped implementation tasks via a single orchestrator. [Meet your team here](https://github.com/alvinunreal/oh-my-opencode-slim#meet-the-pantheon).
- **[Practical engineering experience](docs/rules/technology.md)** along with a composable skillset provided by [Superpowers](https://github.com/obra/superpowers).


## 1. Installation

**Prerequisites** **Bun** v1.3+

1. [Install](https://opencode.ai/docs#install) `OpenCode` and [configure](https://opencode.ai/docs/#configure) your LLM provider(s).
2. Start a new OpenCode session and paste the following prompt:

```text
Fetch and follow instructions from https://raw.githubusercontent.com/jimzhan/rex/refs/heads/main/INSTALL.md
```

> [!TIP]
> Configured API keys are stored in `$HOME/.local/share/opencode/auth.json`. It's recommended to start with a free model for your initial test runs.


## 2. End-to-End Workflow

### 2.1 Development Lifecycle

The following OpenCode slash-commands guide you through the entire development lifecycle:

```mermaid
---
config:
  look: handDrawn
  theme: forest
---
flowchart LR
  Think["<b>/think</b> <i>what's required</i>"]
  Build["<b>/build</b> <i>against the plan</i>"]
  Review["<b>/review</b> <i>implementations</i>"]
  Ship["<b>/ship</b> to <i>production</i>"]

  Think --> Build
  Build --> Review
  Review --> Ship
```


### 2.2 Commands

- `/think` serves as the engine of entire workflow with the following sequential steps:
  - ***Isolate*** - a dedicated workspace using Git worktree to keep changes sandboxed.
  - ***Explore*** - your intent via one of these input types: *`<ticket-url | local-file-path | free-text>`*.
  - ***Design*** - a comprehensive technical design specification and break it down into granular, executable tasks.

- `/build` implements against the structural execution plan.


## 3. Customization

- ***Agents Team*** - create your preset in `.opencode/oh-my-opencode-slim.jsonc` to specify the model, temperature, variants, skills, and MCPs for each agent.
  - `temperature` - standard LLM sampling parameter, controls ***how*** the agent says things (rigid vs. flexible).
  - `variant` - specific to `opencode`, controls ***how hard*** (with more tokens) the agent thinks (shallow vs. deep).
- ***Project Context***
  - Define your prject context in `docs/context.md`.
  - Incorporate your detailed technology standards in `.opencode/always-on/technology.md` ***if deemed necessary***.


> [!TIP]
> Not included, but highly recommended:
>
> - [`rtk`](https://github.com/rtk-ai/rtk) - High-performance CLI proxy that reduces LLM token consumption by 60-90% (`rtk init -g --opencode `).
