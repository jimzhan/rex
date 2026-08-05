<a href="#"><img alt="rex" src="https://raw.githubusercontent.com/goanywhere/rex/assets/images/rex.png" width="160px" height="64px"></a>
===
***Rex*** is an opinionated AI-powered boilerplate designed for model-agnostic and Multi-Agent System (MAS) AI engineering. Built entirely on top of the `OpenCode` ecosystem, it provides battlefield-tested defaults to ship distributed web applications faster.

***What's included?***

- **[OpenCode](https://github.com/anomalyco/opencode)** – Model-agnostic agent orchestration.
  - **[Oh-my-opencode-slim](https://github.com/alvinunreal/oh-my-opencode-slim)** – A Multi-Agent System (MAS) for OpenCode, featuring a specialized agent team that scans codebases, fetches docs, audits architecture, builds UI, and runs scoped implementation tasks via a single orchestrator. [Meet your team here](https://github.com/alvinunreal/oh-my-opencode-slim#meet-the-pantheon).
- **[Practical engineering experience](docs/rules/technology.md)*** along with a composable skillset provided by [Superpowers](https://github.com/obra/superpowers).


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
  Build["<b>/build</b> <i>what's required</i>"]
  Review["<b>/review</b> <i>implementations</i>"]
  Ship["<b>/ship</b> to <i>production</i>"]

  Build --> Review
  Review --> Ship
```


### 2.2 Commands

- `/build` serves as the engine of the entire workflow. When invoked, it executes the following sequential steps:
  1. **Isolate** – Create a dedicated workspace using Git worktree to keep changes sandboxed.
  2. **Explore** – Begin by specifying your intent via one of these input types: *`<issue-url | local-file-path | free-text>`*.
  3. **Design** – Generate a comprehensive technical design specification and break it down into granular, executable tasks.
  4. **Implement** – Execute the generated tasks to produce the final implementation.


## 3. Customization

### 3.1 oh-my-opencode-slim

The default MAS preset is `opencode`  with free models provided by `OpenCode`. To maximize the capabilities of your subscribed AI models, create a custom preset in `.opencode/oh-my-opencode-slim.jsonc` to specify the model, temperature, variants, skills, and MCPs for each agent. ***Example***

```json
{
  "preset": "gpt-5.6-codex",
  "presets": {
    "gpt-5.6-codex": {
      "orchestrator": { "model": "openai/gpt-5.6-terra", "temperature": 0.4, "skills": ["*"], "mcps": ["*", "!context7"] },
      "oracle":       { "model": "openai/gpt-5.6-sol", "temperature": 0.4, "variant": "max", "skills": ["simplify"], "mcps": [] },
      "explorer":     { "model": "openai/gpt-5.6-luna", "temperature": 0.2, "skills": [], "mcps": [] },
      "librarian":    { "model": "openai/gpt-5.6-luna", "temperature": 0.2, "skills": [], "mcps": ["websearch", "context7", "gh_grep"] },
      "designer":     { "model": "openai/gpt-5.6-terra", "temperature": 0.3, "variant": "medium", "skills": [], "mcps": [] },
      "fixer":        { "model": "openai/gpt-5.6-terra", "temperature": 0.2, "variant": "high", "skills": [], "mcps": [] },
      "observer":     { "model": "openai/gpt-5.6-luna", "temperature": 0.2, "variant": "low", "skills": [], "mcps": [] }
    }
  }
}
```

> [!TIP]
>
> `temperature` - standard LLM sampling parameter, controls ***how*** the agent says things (rigid vs. flexible).
>
> `variant` - specific to `opencode`, controls ***how hard*** (with more tokens) the agent thinks (shallow vs. deep).



### 3.2 Project Spec

- Define your prject context in `docs/context.md`.
- Incorporate your detailed technology standards in `docs/rules/technology.md` ***if deemed necessary***.


### 3.3 Extras

> [!TIP]
> Not included, but highly recommended:
>
> - [`rtk`](https://github.com/rtk-ai/rtk) - High-performance CLI proxy that reduces LLM token consumption by 60-90% (`rtk init -g --opencode `).
