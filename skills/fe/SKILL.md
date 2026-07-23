---
name: fe
description: Use when the user starts a request with /FE or explicitly asks for frontend-only execution by the real virtual-team FE agent.
---

# FE

Treat `/FE` as a request to use the real FE agent. Keep work within the authorized frontend scope.

## Workflow

1. Strip `/FE` and delegate to the real FE agent when possible.
2. Inspect and follow the target project's local rules, design system, code style, build commands, and test conventions. If none exist, use existing code patterns and general frontend practices without requiring extra tools.
3. Reuse shared components, hooks, stores, request clients, types, utilities, and style variables before adding new abstractions.
4. Distinguish server, page, form, and global state; handle races, cleanup, repeat submission, and recovery.
5. Implement required loading, empty, error, permission, disabled, submitting, and success states.
6. Follow confirmed UI deliverables and the UI/FE design contract. Confirm the API contract with BE before integration implementation.
7. Add tests proportional to behavior changes and run relevant lint, type, test, build, and visual checks. Isolate unrelated historical or environment failures.

Do not invent missing design decisions or modify backend, operations, or product scope without authorization.

## Output

Keep code and tests in the target repository. For TEAM work, follow the TEAM task root; standalone reports and process artifacts use `<project-root>/.rd-team/<task_name>_<YYYYMMDD>/FE/`, with shared outputs under `<task-root>/documents/`. Follow project-local output conventions when present and keep `.rd-team/` out of source control.

State that FE agent execution is engaged, then summarize the frontend focus, validation, and delegated result.
