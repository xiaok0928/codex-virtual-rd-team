---
name: rd-team-routing
description: Route virtual R&D requests to the smallest safe set of real PM, UI, SA, TPM, BE, FE, QA, and SRE agents. Use when team, bf, or a coordinating virtual-team workflow must select roles, enforce contract gates, decide whether planning-with-files is eligible, or establish the canonical ai-doc task and delivery paths. Do not use for ordinary single-agent work.
---

# R&D Team Routing

## Workspace configuration

Read `~/.codex/AGENTS.md` first, resolve `DEFAULT_PROJECT_WORKSPACE`, and normalize it to an absolute path without a trailing slash. Use it as the default delivery root for `ai-doc`, virtual-team, planning, and delivery outputs. A delivery workspace explicitly supplied by the user overrides it for the current request. Do not infer the affected source repository from this path.

Route work to real virtual-team agents. Never simulate a selected role.

## Canonical paths

Use the default project workspace for every virtual-team artifact:

```text
Task root: ${DEFAULT_PROJECT_WORKSPACE}/ai-doc/virtual-team/<task_name>_<YYYYMMDD>/
Role output: <task-root>/<ROLE>/
Version output: <task-root>/versions/<version>/<ROLE>/
Shared output: <task-root>/documents/
Planning: <task-root>/planning-with-files/
Delivery record: owned by `record-delivery` under the resolved delivery workspace
```

Create the task root before delegating. Never fall back to a project repository, product root, Codex session directory, or `.local/` directory. If a role's sandbox cannot write the canonical path, have that role return its artifact to the main coordinator and let the coordinator persist it there.

## Routes

- `backend_only_small`: BE. Apply the global and applicable project-level `AGENTS.md` development rules.
- `frontend_only_small`: FE. Add UI only when the design contract is not already settled.
- `ui_only_small`: UI.
- `fullstack_small`: BE + FE. Confirm the API contract before parallel implementation.
- `ui_frontend_small`: UI + FE. Confirm the design contract before FE implementation.
- `product_unclear`: PM, then TPM if implementation decomposition is needed.
- `architecture_risk`: PM + SA + TPM plus relevant implementation roles.
- `testing_risk`: QA added to the smallest applicable route.
- `sre_risk`: SRE added when deployment, reliability, runtime, observability, rollback, or secrets are affected.
- `large_cross_module`: use the full `team` workflow.

Prefer the smallest role set that safely covers the work. Do not add roles merely because they are available.

## Gates

1. PM confirms product scope and acceptance criteria when semantics are unclear.
2. UI and SA may work in parallel after PM confirmation when both are relevant.
3. TPM decomposes execution only after UI is confirmed or skipped and SA is confirmed.
4. UI deliverables require PM review, user confirmation, then a UI/FE design contract.
5. BE and FE confirm the API contract before integration implementation.
6. QA cases require relevant-role review; PM and SA resolve disputed product or boundary expectations.
7. Repeat test, fix, and retest until agreed cases pass or an unrelated/environment failure is explicitly isolated.

## Planning eligibility

Activate `planning-with-files` only when real virtual-team agents are engaged and confirmed implementation is complex and multi-stage. Do not activate it for requirements, PRDs, architecture discussion, consultation, documentation-only work, narrow implementation, or ordinary single-agent execution.

## Validation and delivery

- Require validation proportional to the changed scope.
- Require all tests and checks affected by the change to pass.
- Isolate unrelated historical or environment failures instead of expanding scope.
- After eligible implementation and final validation, invoke `record-delivery` once for the shared requirement, not per role or iteration.
- Let `record-delivery` own deduplication, existing-record updates, timestamps, and validation evidence.
