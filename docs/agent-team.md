# Agent team

The custom agent team for Mona's Project Pulse dashboard is orchestrated by **Orchestrator** (`Claude Opus 5.5 (copilot)`), defined in `.github/agents/orchestrator.agent.md`. It coordinates the specialist agents, assigns non-overlapping work, manages dependencies and integration, and reports the outcome.

| Agent | Target model | Responsibility | Definition |
|---|---|---|---|
| Planner | Claude Opus 5.5 (copilot) | Researches the codebase, dependencies, requirements, and edge cases, then provides an implementation plan. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.7 Flash (copilot) | Guides the dashboard’s UI/UX, accessibility, information hierarchy, interactions, responsive behavior, and visual design. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements assigned code and runnable-app support, with clear errors and validation. | `.github/agents/coder.agent.md` |

I am using **GitHub Copilot CLI in a Codespace** to orchestrate the work with this custom agent team.
