---
name: be
description: Use when the user starts a request with /BE or explicitly asks for backend-only execution by the real virtual-team BE agent.
---

# BE

Use this skill when the user starts a request with `/BE` or explicitly asks for backend-only work.

## Agent Delegation

Treat `/BE` as a request to use the real virtual-team BE agent. If multi-agent tools are available, delegate to the current runtime's BE agent type, such as `be` after agent reload or `backend-developer` in older loaded sessions. The main agent coordinates and summarizes; it should only handle BE work locally when agent delegation is unavailable, and must say so.

## Workflow

1. Strip the `/BE` prefix and treat the remainder as the work item.
2. Delegate the work to the real BE agent when possible.
3. Focus on backend implementation, API changes, data access, backend tests, performance safeguards, or backend bug fixes.
4. Follow the target project's local development guidance, build commands, and test conventions when present. If none exist, use the existing code style and general backend engineering practices without requiring extra tools.
5. Keep the role scoped to backend unless the user explicitly expands the work.

## Output Locations

For TEAM work, follow the TEAM Output Locations rule. BE-owned artifacts go under `BE/`, and cross-role or shared final artifacts go under `documents/`.

When working inside a project repository, use:

```text
.rd-team/BE/<task_name>_<YYYYMMDD>/
```

Keep `.rd-team/` out of source control. For Git projects without an existing ignore rule, prefer the local `.git/info/exclude` unless the project explicitly wants a shared `.gitignore` rule.

If the project defines local output or delivery-record conventions, follow them. Otherwise, do not require an additional delivery record.

## Output

State that BE agent execution is engaged, then summarize the backend focus and delegated result.
