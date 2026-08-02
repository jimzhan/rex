<a href="#"><img alt="rex" src="https://raw.githubusercontent.com/goanywhere/rex/assets/images/rex.png" width="160px" height="64px"></a>
===
***Rex*** is an opinionated AI-powered application development boilerplate built for model-agnostic and Multi-Agent System (MAS) AI engineering. ***What's included?***

- **[OpenCode](https://github.com/anomalyco/opencode)** - Model-agnostic agent orchestration.
  - [Oh-my-opencode-slim](https://github.com/alvinunreal/oh-my-opencode-slim) - A Multi-Agent System (MAS) for OpenCode, featuring a specialized agent team built-in to scan codebases, fetch docs, audit architecture, build UI, and run scoped implementation tasks via a single orchestrator. Meet your team [here](https://github.com/alvinunreal/oh-my-opencode-slim#meet-the-pantheon).
- **[Superpowers](https://github.com/obra/superpowers)** - a set of composable skills and battlefield tested instructions covering:
  1. Architecture
  2. Technology Stack
  3. Database
  4. OpenAPI
  5. Environment
  6. Testing
  7. Git
  8. Deployment


### 1. Installation

- [Install](https://opencode.ai/docs#install) `OpenCode` and [configure](https://opencode.ai/docs/#configure) your LLM provider(s).
- *Paste* the following instructions in `OpenCode`.

```text
Fetch and follow instructions from https://raw.githubusercontent.com/jimzhan/rex/refs/heads/main/INSTALL.md
```
> [!TIP]
> Configured keys are stored in `$HOME/.local/share/opencode/auth.json`. It's recommended to start with the free model for your initial test runs.


### 2. End-to-End Workflow

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
