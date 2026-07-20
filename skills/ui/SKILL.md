---
name: ui
description: Use when the user starts a request with /UI or when the virtual team needs visual design, UI page design, design assets, slicing, design specs, or UI deliverables by the real virtual-team UI agent.
---

# UI

Use this skill when the user starts a request with `/UI` or when the virtual team needs UI design support.

## Agent Delegation

Treat `/UI` as a request to use the real virtual-team UI agent. If multi-agent tools are available, delegate to the current runtime's UI agent type, such as `ui` after agent reload. The main agent coordinates and summarizes; it should only handle UI work locally when agent delegation is unavailable, and must say so.

## Responsibilities

- Define visual direction: colors, typography, icon style, component feel, spacing scale, and cross-platform consistency.
- Design HTML page or page set based on PM PRD and current-version scope.
- Prepare icons, images, sliced assets, and design specs.
- Annotate dimensions, spacing, color codes, typography, image usage, component states, empty/loading/error states, and interactions.
- Write handoff documentation for FE.

## Workflow

1. Strip the `/UI` prefix and treat the remainder as the work item.
2. Delegate the work to the real UI agent when possible.
3. Identify product version from PM PRD or user request; if missing, use `v0.1` and note the assumption.
4. Define or extend visual direction, then design required HTML pages.
5. Export assets, annotate specs, and write handoff documentation.
6. Submit UI deliverables to PM; update until PM and UI agree, then wait for user confirmation before FE implementation.

## Output Locations

For product-version output:

```text
<product-root>/<YYYYMMDD>_<version>/UI/
```

For project-local execution artifacts:

```text
<project-root>/.local/team/UI/<task_name>_<YYYYMMDD>/
```

UI-owned artifacts such as visual guidelines, page designs, sliced assets, specs, and handoff notes go under `UI/`. Cross-role UI confirmation records may also go under `documents/`.

## Deliverables

- `visual-guidelines.md`
- `pages/`
- `assets/`
- `specs.md`
- `README.md`

If the project defines local output or delivery-record conventions, follow them. Otherwise, do not require an additional delivery record.

## Output

State that UI agent execution is engaged, then summarize visual direction, page deliverables, asset deliverables, output folder, and delegated result.
