---
name: be
description: Use when the user starts a request with /BE or explicitly asks for backend-only execution by the real virtual-team BE agent.
---

# BE

## Workspace configuration

Read `~/.codex/AGENTS.md` first, resolve `DEFAULT_PROJECT_WORKSPACE`, and normalize it to an absolute path without a trailing slash. Use it as the default delivery root for `ai-doc`, virtual-team, planning, and delivery outputs. A delivery workspace explicitly supplied by the user overrides it for the current request. Do not infer the affected source repository from this path.

Use this skill when the user starts a request with `/BE` or explicitly asks for backend-only work.

## Agent Delegation

Treat `/BE` as a request to use the real virtual-team BE agent. If multi-agent tools are available, delegate to the current runtime's BE agent type, such as `be` after agent reload or `backend-developer` in older loaded sessions. The main agent coordinates and summarizes; it should only handle BE work locally when agent delegation is unavailable, and must say so.

## Workflow

1. Strip the `/BE` prefix and treat the remainder as the work item.
2. Delegate the work to the real BE agent when possible.
3. Focus on backend implementation, API changes, data access, backend tests, performance safeguards, or backend bug fixes.
4. Apply the global and applicable project-level `AGENTS.md` development rules to backend implementation.
5. Keep the role scoped to backend unless the user explicitly expands the work.

## Output Locations

For TEAM work, follow the TEAM Output Locations rule. For standalone BE work, store BE-owned artifacts under:

```text
${DEFAULT_PROJECT_WORKSPACE}/ai-doc/virtual-team/<task_name>_<YYYYMMDD>/BE/
```

Store cross-role or shared final artifacts under the same task root's `documents/` directory.

For an eligible standalone BE delivery, use `record-delivery` once at the requirement level after implementation and validation. Do not create one record per agent or role. Do not write BE artifacts to the project repository or `.local/` directories.

## Output

State that BE agent execution is engaged, then summarize the backend focus and delegated result.
