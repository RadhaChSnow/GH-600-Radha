# Project Pulse dashboard implementation plan

## Goal and repository context

Build a polished, responsive Project Pulse dashboard for Mona. The repository currently has no `app/` directory, application dependencies, or app-specific test/build setup, so implement this as a small static frontend unless implementation research establishes a necessary alternative. Keep it easy to run in the Codespace and avoid adding dependencies without a clear need.

The dashboard should present project status and priority clearly, with accessible structure, responsive behavior, and deterministic styling hooks such as `.dashboard` and `.project-card`. Keep project content in JSON and render it from the page. Because browsers restrict fetching local JSON from a `file://` URL, serve the app over HTTP for development and preview.

## Agent responsibilities and file assignments

| Agent | Responsibilities | Files |
|---|---|---|
| **Designer** | Define and implement the visual system, responsive layout, readable hierarchy, status/priority treatments, and accessible interaction states. Coordinate class names with the page structure and avoid changing application logic. | `app/styles.css` |
| **Coder** | Implement semantic page structure, load and render project data, create representative deterministic data, configure a runnable Codespace preview, integrate the Designer's styles, and validate the result. | `app/index.html`, `app/project-data.json`, `.vscode/launch.json` |
| **Planner** | Research repository conventions and requirements, agree the data and selector contract before implementation, and identify risks and validation expectations. | Planning only; no application files. |
| **Orchestrator** | Coordinate the handoff, keep file ownership clear, resolve integration issues, and verify the final dashboard against the goal. | No implementation files. |

## Shared implementation contract

- Store dashboard content in `app/project-data.json`. Agree on the project fields before parallel implementation; include only fields needed to display the dashboard (for example, project name, status, priority, owner, and a concise progress or due-date detail).
- Use semantic HTML and accessible names/labels. The page should load the JSON, render project cards, and communicate a useful loading or error state if data cannot be loaded.
- The stylesheet owns the visual treatment and responsive layout. Keep `.dashboard` and `.project-card` stable as shared hooks, and coordinate any additional selectors with the Coder.
- The launch configuration should run the app from `${workspaceFolder}/app` and open `index.html` through an HTTP-served preview so the JSON fetch works. Use a deterministic command, port, and URL supported by the Codespace environment.

## Work phases, dependencies, and parallelism

1. **Agree on interfaces (sequential prerequisite).** The Orchestrator confirms the JSON fields, HTML-to-CSS class hooks, and preview approach with Designer and Coder. These shared contracts prevent mismatched data and selectors.
2. **Build independent pieces (parallel).** Once the contracts are set, Designer implements `app/styles.css`. In parallel, Coder creates `app/project-data.json`, `app/index.html`, and `.vscode/launch.json`. The files have separate owners, and the agreed contract allows the page and styles to be developed without a file conflict.
3. **Integrate and validate (sequential).** Coder and Designer resolve any mismatch between rendered markup and styles. The Orchestrator checks the complete page and preview setup together; fix integration issues before considering the work complete.

The shared interface agreement must precede parallel work. Integration and end-to-end preview validation depend on all four assigned files being present.

## Validation expectations

- Check that `app/index.html` loads `app/project-data.json` when served over HTTP, renders the expected project content, and handles loading or fetch failures without silently presenting a successful empty dashboard.
- Verify the markup is semantic and keyboard accessible, status and priority are understandable without color alone, and the layout remains readable at narrow and wide viewport sizes.
- Confirm the CSS hooks match the generated markup and the page has the intended Project Pulse visual hierarchy.
- Parse `app/project-data.json` and `.vscode/launch.json` as valid JSON; confirm the launch configuration uses the `app` working directory and opens the dashboard through the selected HTTP preview.
- Run the configured preview in the Codespace and inspect the browser result. Since the repository has no existing app test or build tooling, do not add a framework or test dependency solely for this dashboard; add focused automated checks only if implementation introduces a suitable existing runner.
