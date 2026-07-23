---
name: bf
description: Use when the user starts a request with /BF or asks for a small frontend/backend delivery path using the real virtual-team BE and FE agents.
---

# BF

Use for `/BF` small frontend/backend delivery.

## Agent Delegation

Treat `/BF` as a request to coordinate real virtual-team agents, not as a request for the main agent to simulate BE/FE work.

- Use real BE and FE agents for `fullstack_small`.
- Use real BE agent for `backend_only_small`.
- Use real FE agent for `frontend_only_small`.
- Current runtime agent names may be `be`/`fe` after agent reload, or `backend-developer`/`frontend-developer` in older loaded sessions.
- The main agent coordinates routing, interface alignment, progress tracking, conflict resolution, integration validation, and final summary.
- If multi-agent delegation is unavailable, clearly state the fallback before doing the work locally.

## Workflow

1. Strip the `/BF` prefix and treat the remainder as the actual work request.
2. Use the `rd-team-routing` skill to choose the smallest safe route and task root.
3. Prefer `fullstack_small` when the change needs both frontend and backend.
4. Fall back to `backend_only_small` or `frontend_only_small` when only one side is needed.
5. Follow each target project's local development guidance, build commands, and test conventions when present. If none exist, use existing code style and general engineering practices without requiring extra tools.
6. For `fullstack_small`, run two phases:
   - Interface alignment: real BE and FE agents first confirm the API contract together, including route, method, request parameters, response shape, error states, auth/permission needs, and pagination/filter/sort behavior when relevant.
   - Parallel development: after both agents confirm the API contract, BE and FE develop in parallel. BE owns backend interfaces, services, data handling, and targeted tests. FE owns UI implementation, state, API calls, interaction feedback, and targeted validation.
7. The main agent tracks both agents, merges results, resolves integration conflicts, and performs final integration validation.
8. Ask one concise clarification only when scope or API contract cannot be inferred safely.

## Guardrails

- Prefer real BE and FE agents only.
- Do not add PM, SA, QA, TPM, UI, or SRE unless the request clearly needs them.
- Do not start BE and FE implementation before the shared API contract is confirmed.
- Use parallel BE/FE development after interface alignment unless work is single-sided, both roles must modify the same files/modules, or one side has a hard dependency on the other's completed implementation.

## Output Locations

Store BF artifacts under one task root unless the target project defines another convention:

```text
<project-root>/.rd-team/<task_name>_<YYYYMMDD>/
```

Use `<task-root>/BE/`, `<task-root>/FE/`, and `<task-root>/documents/` for role and shared outputs. For eligible complex multi-stage work, use `<task-root>/planning-with-files/`. Keep `.rd-team/` out of source control, preferably through the project's local `.git/info/exclude`.

## Output

State that BF agent collaboration is engaged, name the selected route, identify the real agents used, and summarize the result.
