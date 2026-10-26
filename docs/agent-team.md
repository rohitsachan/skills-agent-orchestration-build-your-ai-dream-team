# Project Pulse agent team

The custom team in `.github/agents/` gives us a clear division of labor for the Project Pulse dashboard:

- Orchestrator — Model: Claude Opus 5.5. Responsibility: coordinates the overall request, breaks the work into phases, delegates to specialists, keeps file ownership clear, and checks that the final result fits together. File: `.github/agents/orchestrator.agent.md`.
- Planner — Model: Claude Opus 5.5. Responsibility: researches the repo, identifies dependencies and risks, and creates the implementation plan with ordered steps, file assignments, validation expectations, and open questions. File: `.github/agents/planner.agent.md`.
- Coder — Model: GPT-5.5. Responsibility: implements the code, creates deterministic support files when needed, and validates the app behavior within the assigned file scope. File: `.github/agents/coder.agent.md`.
- Designer — Model: Gemini 3.7 Flash. Responsibility: shapes the experience, visual hierarchy, accessibility, and polished dashboard styling so the app looks like a finished Project Pulse frontend. File: `.github/agents/designer.agent.md`.

The team will work together as follows: the Orchestrator receives the request and delegates planning to the Planner. The Planner creates a phased implementation strategy and file ownership map. Then the Orchestrator coordinates the Designer and Coder in clear, scoped workstreams so they do not overwrite each other. The Designer focuses on the UI structure and visual polish, while the Coder implements the actual dashboard data and app files. Finally, the Orchestrator reviews the combined result and confirms the dashboard is consistent, complete, and ready to hand off.