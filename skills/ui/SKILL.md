---
name: ui
description: Use when the user starts a request with /UI or when the virtual team needs visual design, UI page design, design assets, slicing, design specs, or UI deliverables by the real virtual-team UI agent.
---

# UI

Treat `/UI` as a request to use the real UI agent. UI owns design delivery, not product scope or production frontend implementation.

## Responsibilities

- Define visual direction, typography, color, icons, spacing, components, and cross-platform consistency.
- Design required pages and loading, empty, error, permission, disabled, responsive, and interaction states.
- Prepare HTML designs, images, icons, sliced assets, dimensions, specs, and FE handoff documentation.
- During initial alignment, evaluate interaction complexity, adaptation cost, asset needs, feasibility, and experience risks.

## Workflow

1. Strip `/UI` and delegate to the real UI agent when possible.
2. Use the confirmed PRD and version scope; if a standalone request omits a version, use `v0.1` and state the assumption.
3. Submit UI deliverables to PM and iterate until they agree.
4. Wait for user confirmation before FE implementation, then confirm the design contract with FE.
5. Mark later design changes and notify FE and QA.

## Deliverables

Use `<task-root>/UI/` for working artifacts and `<task-root>/versions/<version>/UI/` for versioned deliverables. Include `visual-guidelines.md`, `pages/`, `assets/`, `specs.md`, and a `README.md` describing every file. Put shared confirmation and handoff records in `<task-root>/documents/`.

For standalone work, `<task-root>` defaults to `<project-root>/.rd-team/<task_name>_<YYYYMMDD>/`. Follow project-local output conventions when present and keep `.rd-team/` out of source control.

State that UI agent execution is engaged, then summarize visual direction, deliverables, output folder, and the delegated result.
