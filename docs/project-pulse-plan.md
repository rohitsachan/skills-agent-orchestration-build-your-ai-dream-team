# Project Pulse Dashboard Plan

## Summary

Create a responsive, accessible Project Pulse dashboard as a small static app. The repository does not currently define dashboard requirements, data fields, or an `app/` directory, so the initial content and data model below are proposals to confirm—not requirements supplied by the user. Keep the implementation deterministic and self-contained; do not add a framework or dependencies unless a later decision requires them.

## Ownership and file scope

| Owner | Files | Responsibilities |
| --- | --- | --- |
| Coder | `app/index.html` | Semantic page structure, accessible labels and landmarks, and rendering/reading the project data. Provide the agreed `.dashboard` and `.project-card` hooks for styling. |
| Designer | `app/styles.css` | Visual design, responsive layouts, focus/hover states, and accessible contrast. Style the agreed `.dashboard` and `.project-card` hooks. |
| Coder | `app/project-data.json` | Deterministic sample project data in the schema agreed with Designer and project stakeholders. |
| Coder | `.vscode/launch.json` | Strict-JSON VS Code launch configuration with working directory `${workspaceFolder}/app` and entry point `${workspaceFolder}/app/index.html`. |

These scopes must not overlap: Designer owns CSS; Coder owns HTML, JSON data, and launch configuration. Both agents should edit only their assigned files.

## Ordered phases

1. **Confirm the contract (sequential; before implementation).** Designer and Coder agree on the dashboard regions, `.dashboard` and `.project-card` hooks, responsive behavior, and the JSON field names/types needed by the HTML and styles. Confirm any available stakeholder expectations for metrics, project content, and interactions. The repository currently supplies none; if no further requirements are provided, document a minimal, clearly identified sample dataset and avoid presenting it as authoritative business data.
2. **Build the independent files (parallel after Phase 1).** Designer implements `app/styles.css` against the agreed hooks and layout. Coder implements `app/index.html`, `app/project-data.json`, and `.vscode/launch.json` against the same agreed contract. No file has two owners. Coder should ensure the page can load the static JSON in the intended local preview environment; if that environment imposes restrictions, surface them rather than silently adding tooling.
3. **Integrate and validate (sequential).** Review the page, data, and styles together; resolve mismatches through the owning agent for each file. Exercise the launch configuration and perform the checks below. Update the plan or implementation contract if a confirmed requirement changes scope.

## Dependencies and parallelism

- Phase 1 is a prerequisite for both implementation assignments: parallel work before agreement risks mismatched class hooks, layout assumptions, and JSON property names.
- After the contract is agreed, Designer's CSS and Coder's HTML/data/config work can proceed in parallel because their file scopes are disjoint.
- Final integration depends on both assignments being complete and is sequential so the combined page can be checked against the shared contract.
- `.vscode/tasks.json` currently contains only an exercise terminal task; do not treat it as an app runner or modify it as part of this plan.

## Assumptions and risks

- There is no existing `app/` directory, and `README.md` does not specify app behavior or dashboard requirements.
- The project data, displayed measures, empty/error states, and any user interactions remain to be confirmed. Use representative sample content only if needed to demonstrate the layout; label it as sample content.
- The static JSON loading approach must work in the selected local preview/browser context. Opening a file directly may restrict `fetch`; validate the chosen launch path and use an already available local server if one exists. Do not add a dependency or task without an explicit need.
- The `.dashboard` and `.project-card` selectors are expected integration hooks. Other markup and data details are intentionally left to the Phase 1 agreement.
- The launch configuration's browser/debugger type may depend on installed VS Code extensions. Confirm the available debugger before choosing a type; keep the configuration strict JSON, use `${workspaceFolder}/app` as `cwd`, and target `${workspaceFolder}/app/index.html`.

## Validation expectations

- Confirm all four planned implementation files exist in their assigned locations and no file-scope ownership overlaps.
- Parse `app/project-data.json` as JSON and verify its records conform to the schema agreed in Phase 1; check that the HTML consumes the same property names.
- Parse `.vscode/launch.json` as strict JSON (no comments or trailing commas); verify its working directory and entry point resolve to the specified app paths and the selected debugger is available.
- Open the page through the documented launch/preview path. Check that sample data renders, the `.dashboard` and `.project-card` hooks are present, and there are no missing assets or console errors.
- Inspect narrow and wide viewport layouts, keyboard navigation and visible focus, semantic landmarks/heading order, accessible names, and text/background contrast. Confirm long or missing sample values do not break the layout.
