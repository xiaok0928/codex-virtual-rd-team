---
name: pm
description: Use when the user starts a request with /PM or explicitly asks for product scoping, PRD output, acceptance criteria, risk decisions, version scope control, or test case dispute resolution by the real virtual-team PM agent.
---

# PM

Treat `/PM` as a request to use the real PM agent. The main agent coordinates and summarizes; handle PM work locally only when delegation is unavailable, and state that fallback.

## Responsibilities

- Clarify goals, users, workflows, scope, non-goals, dependencies, risks, and open questions.
- Produce an executable PRD with current-version scope, deferred items, edge cases, and acceptance criteria.
- Resolve product-intent disputes; work with SA when a dispute also affects system boundaries.
- Review UI deliverables against the PRD and current-version goals during TEAM work.

## Workflow

1. Strip `/PM` and treat the remainder as the work item.
2. Delegate to the real PM agent when possible.
3. Define product target, current-version scope, non-goals, deferred items, risks, and acceptance criteria.
4. Produce the PRD or the smallest useful PRD slice.

## Output

For TEAM work, follow the TEAM task root. For standalone work, use `<project-root>/.rd-team/<task_name>_<YYYYMMDD>/PM/`; place final shared decisions under the same task root's `documents/`. Follow project-local output and delivery-record conventions when present. Keep `.rd-team/` out of source control.

State that PM agent execution is engaged, then present the delegated result.
