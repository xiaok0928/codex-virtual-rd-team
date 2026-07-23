---
name: rd-team-routing
description: Route virtual R&D requests to the smallest safe set of real PM, UI, SA, TPM, BE, FE, QA, and SRE agents. Use when team, bf, or another coordinating virtual-team workflow must select roles, enforce contract gates, decide whether file-based planning is warranted, or establish portable task output paths. Do not use for ordinary single-agent work.
---

# R&D Team Routing

Route work to real virtual-team agents. Never simulate a selected role.

## Project Conventions

Before routing implementation work, inspect the target project's `AGENTS.md`, `Agent.md`, contribution guide, engineering documentation, build scripts, test commands, output rules, and other local conventions. Follow them when present. If the project has no local conventions, continue with its existing patterns and general engineering practices without requiring extra skills, tools, directories, or planning files.

## Portable Paths

Unless the target project defines another output convention, use one project-local task root:

```text
Task root: <project-root>/.rd-team/<task_name>_<YYYYMMDD>/
Role output: <task-root>/<ROLE>/
Version output: <task-root>/versions/<version>/<ROLE>/
Shared output: <task-root>/documents/
Planning: <task-root>/planning-with-files/
```

Keep `.rd-team/` out of source control. For Git projects without an existing ignore rule, prefer the local `.git/info/exclude`; change the tracked `.gitignore` only when the user or project explicitly wants a shared rule. Create the task root before delegation. If a role cannot write there, have it return the artifact to the main coordinator for persistence instead of inventing another path.

## Routes

- `backend_only_small`: BE.
- `frontend_only_small`: FE. Add UI only when the design contract is not settled.
- `ui_only_small`: UI.
- `fullstack_small`: BE + FE. Confirm the API contract before parallel implementation.
- `ui_frontend_small`: UI + FE. Confirm the design contract before FE implementation.
- `product_unclear`: PM, then TPM when implementation decomposition is needed.
- `architecture_risk`: PM + SA + TPM plus relevant implementation roles.
- `testing_risk`: add QA to the smallest applicable route.
- `sre_risk`: add SRE when deployment, reliability, runtime, observability, rollback, or secrets are affected.
- `large_cross_module`: use the full `team` workflow.

Prefer the smallest role set that safely covers the work. Do not add roles merely because they are available.

## Gates

1. PM confirms product scope and acceptance criteria when semantics are unclear.
2. UI and SA may work in parallel after PM confirmation when both are relevant.
3. TPM decomposes execution only after UI is confirmed or skipped and SA is confirmed.
4. UI deliverables require PM review, user confirmation, then a UI/FE design contract.
5. BE and FE confirm the API contract before integration implementation.
6. QA cases require relevant-role review; PM and SA resolve disputed product or boundary expectations.
7. Repeat test, fix, and retest until agreed cases pass or an unrelated environment failure is explicitly isolated.

## Planning Eligibility

Use file-based planning only when real virtual-team agents are engaged and confirmed implementation is complex and multi-stage. Do not require it for requirements, PRDs, architecture discussion, consultation, documentation-only work, narrow implementation, or ordinary single-agent execution.

## Validation And Delivery

- Require validation proportional to the changed scope.
- Require all checks affected by the change to pass.
- Isolate unrelated historical or environment failures instead of expanding scope.
- Follow project-local delivery-record conventions when present; otherwise do not require an additional delivery record.
