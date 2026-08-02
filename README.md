<a href="#"><img alt="rex" src="https://raw.githubusercontent.com/goanywhere/rex/assets/images/rex.png" width="160px" height="64px"></a>
===
***Rex*** is an opinionated AI-powered boilerplate designed for model-agnostic and Multi-Agent System (MAS) AI engineering. Built entirely on top of the OpenCode ecosystem, it provides battlefield-tested defaults to ship distributed web applications faster.

***What's included?***

- **[OpenCode](https://github.com/anomalyco/opencode)** – Model-agnostic agent orchestration.
  - **[Oh-my-opencode-slim](https://github.com/alvinunreal/oh-my-opencode-slim)** – A Multi-Agent System (MAS) for OpenCode, featuring a specialized agent team that scans codebases, fetches docs, audits architecture, builds UI, and runs scoped implementation tasks via a single orchestrator. [Meet your team here](https://github.com/alvinunreal/oh-my-opencode-slim#meet-the-pantheon).
- **[Superpowers](https://github.com/obra/superpowers)** – A composable skillset with critical engineering experience covering:
  - Architecture
  - Technology Stack
  - Database
  - OpenAPI
  - Environment
  - Testing
  - Git
  - Deployment


### 1. Prerequisites

- **Node.js** 20 LTS or higher


### 2. Installation

1. [Install](https://opencode.ai/docs#install) `OpenCode` and [configure](https://opencode.ai/docs/#configure) your LLM provider(s).
2. Start a new OpenCode session and paste the following prompt:

```text
Fetch and follow instructions from https://raw.githubusercontent.com/jimzhan/rex/refs/heads/main/INSTALL.md
```

> [!TIP]
> Configured API keys are stored in `$HOME/.local/share/opencode/auth.json`. We recommend starting with a free model for your initial test runs.


### 3. End-to-End Workflow

The following OpenCode slash-commands guide you through the entire development lifecycle:

```mermaid
---
config:
  look: handDrawn
  theme: forest
---
flowchart LR
  Build["<b>/build</b> <i>what's required</i>"]
  Review["<b>/review</b> <i>implementations</i>"]
  Ship["<b>/ship</b> to <i>production</i>"]

  Build --> Review
  Review --> Ship
```
