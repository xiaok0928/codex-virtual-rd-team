---
name: fe
description: Use when the user starts a request with /FE or explicitly asks for frontend-only execution by the real virtual-team FE agent.
---

# FE

Use this skill when the user starts a request with `/FE` or explicitly asks for frontend-only work.

## Agent Delegation

Treat `/FE` as a request to use the real virtual-team FE agent, not as a request for the main agent to merely follow frontend instructions.

If multi-agent tools are available, delegate to the current runtime's FE agent type, such as `fe` after agent reload or `frontend-developer` in older loaded sessions. The main agent coordinates, passes context, receives the FE result, and summarizes or integrates it. The main agent should only handle FE work locally when agent delegation is unavailable, and must clearly say so.

## Workflow

1. Strip the `/FE` prefix and treat the remainder as the work item.
2. Delegate the work to the real FE agent when possible.
3. Keep FE work focused on UI implementation, client state, component updates, API integration, frontend tests, build checks, or frontend bug fixes.
4. Keep the role scoped to frontend unless the user explicitly expands the work.

## Output Locations

For TEAM work, follow the TEAM Output Locations rule. FE-owned artifacts go under `FE/`, and cross-role or shared final artifacts go under `documents/`.

When working inside a project repository, use:

```text
.rd-team/FE/<task_name>_<YYYYMMDD>/
```

Keep `.rd-team/` out of source control. For Git projects without an existing ignore rule, prefer the local `.git/info/exclude` unless the project explicitly wants a shared `.gitignore` rule.

If the project defines local output or delivery-record conventions, follow them. Otherwise, do not require an additional delivery record.

## Output

State that FE agent execution is engaged, then summarize the frontend focus and delegated result.
