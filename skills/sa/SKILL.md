---
name: sa
description: Use when the user starts a request with /SA or explicitly asks for architecture support by the real virtual-team SA agent.
---

# SA

Use this skill when the user starts a request with `/SA` or explicitly asks for architecture support.

## Agent Delegation

Treat `/SA` as a request to use the real virtual-team SA agent. If multi-agent tools are available, delegate to the current runtime's SA agent type, such as `sa`. The main agent coordinates and summarizes; it should only handle SA work locally when agent delegation is unavailable, and must say so.

## Workflow

1. Strip the `/SA` prefix and treat the remainder as the work item.
2. Delegate the work to the real SA agent when possible.
3. Focus on architecture, module boundaries, cross-service design, system constraints, and risk analysis.
4. Keep the role scoped to architecture unless the user explicitly expands the work.

## Output Locations

For TEAM work, follow the TEAM Output Locations rule. SA-owned artifacts go under `SA/`, and cross-role or shared final artifacts go under `documents/`.

When working inside a project repository, use:

```text
.local/team/SA/<task_name>_<YYYYMMDD>/
```

If the project defines local output or delivery-record conventions, follow them. Otherwise, do not require an additional delivery record.

## Output

State that SA agent execution is engaged, then summarize the architecture focus and delegated result.
