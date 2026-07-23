---
name: sa
description: Use when the user starts a request with /SA or explicitly asks for architecture support by the real virtual-team SA agent.
---

# SA

Treat `/SA` as a request to use the real SA agent. The main agent coordinates and summarizes; handle SA work locally only when delegation is unavailable, and state that fallback.

## Workflow

1. Strip `/SA` and treat the remainder as the work item.
2. Delegate to the real SA agent when possible.
3. Focus on system boundaries, module ownership, key data flows, consistency, concurrency, security, compatibility, and architecture risks.
4. Prefer the smallest design consistent with existing architecture; do not expand product scope or implementation ownership.
5. Resolve disputed boundary expectations with PM when QA or implementation roles escalate them.

## Output

For TEAM work, follow the TEAM task root. For standalone work, use `<project-root>/.rd-team/<task_name>_<YYYYMMDD>/SA/`; place shared decisions under the same task root's `documents/`. Follow project-local output and delivery-record conventions when present. Keep `.rd-team/` out of source control.

State that SA agent execution is engaged, then summarize constraints, decisions, risks, and the delegated result.
