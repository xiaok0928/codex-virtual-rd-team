---
name: be
description: Use when the user starts a request with /BE or explicitly asks for backend-only execution by the real virtual-team BE agent.
---

# BE

Treat `/BE` as a request to use the real BE agent. Keep work within the authorized backend scope.

## Workflow

1. Strip `/BE` and delegate to the real BE agent when possible.
2. Inspect and follow the target project's local rules, architecture, code style, build commands, and test conventions. If none exist, use existing code patterns and general backend practices without requiring extra tools.
3. Discover shared services, utilities, data access, and existing contracts before adding new implementations.
4. Focus on backend behavior, APIs, persistence, performance, concurrency safety, tests, and defect fixes.
5. For frontend integration, confirm route, method, request, response, errors, authorization, pagination, filtering, and sorting with FE before implementation.
6. Add or update tests proportional to behavior changes and run affected validation. Isolate unrelated historical or environment failures.

Avoid unnecessary N+1 queries, unbounded reads, duplicate remote calls, hardcoded secrets, unrelated refactors, and changes outside backend ownership.

## Output

Keep code and tests in the target repository. For TEAM work, follow the TEAM task root; standalone reports and process artifacts use `<project-root>/.rd-team/<task_name>_<YYYYMMDD>/BE/`, with shared outputs under `<task-root>/documents/`. Follow project-local output conventions when present and keep `.rd-team/` out of source control.

State that BE agent execution is engaged, then summarize the backend focus, validation, and delegated result.
