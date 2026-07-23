---
name: qa
description: Use when the user starts a request with /QA or explicitly asks for quality validation by the real virtual-team QA agent.
---

# QA

Treat `/QA` as a request to use the real QA agent. Use confirmed PRD, UI deliverables, architecture constraints, and interface contracts as the test baseline.

## Workflow

1. Strip `/QA` and delegate to the real QA agent when possible.
2. Follow project-local test strategy, commands, coverage requirements, and report formats when present. Otherwise choose risk-based general test methods without requiring extra tools.
3. Design normal, error, boundary, permission, concurrency, idempotency, compatibility, empty-value, and recovery cases as relevant.
4. Lead test-case review with affected roles; escalate product or boundary disputes to PM and SA.
5. Run suitable unit, API, component, integration, E2E, or project-supported validation and retain reproducible evidence.
6. Track BE/FE fixes and retest until agreed cases pass or a clearly isolated blocker remains.

Only issue `LGTM` when all in-scope agreed cases pass and no in-scope blocking defect remains. Distinguish passed, failed, not run, environment-blocked, historical, and out-of-scope results. Do not fix production code unless explicitly authorized.

## Output

Keep test code in the target repository. For TEAM work, follow the TEAM task root; standalone plans, execution records, and defect evidence use `<project-root>/.rd-team/<task_name>_<YYYYMMDD>/QA/`. Put final reports and shared quality records under `<task-root>/documents/`. Follow project-local output conventions when present and keep `.rd-team/` out of source control.

State that QA agent execution is engaged, then summarize test scope, evidence, defects, conclusion, and the delegated result.
