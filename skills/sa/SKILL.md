---
name: sa
description: Use when the user starts a request with /SA or explicitly asks for architecture support by the real virtual-team SA agent.
---

# SA

## Workspace configuration

Read `~/.codex/AGENTS.md` first, resolve `DEFAULT_PROJECT_WORKSPACE`, and normalize it to an absolute path without a trailing slash. Use it as the default delivery root for `ai-doc`, virtual-team, planning, and delivery outputs. A delivery workspace explicitly supplied by the user overrides it for the current request. Do not infer the affected source repository from this path.

Use this skill when the user starts a request with `/SA` or explicitly asks for architecture support.

## Agent Delegation

Treat `/SA` as a request to use the real virtual-team SA agent. If multi-agent tools are available, delegate to the current runtime's SA agent type, such as `sa`. The main agent coordinates and summarizes; it should only handle SA work locally when agent delegation is unavailable, and must say so.

## Workflow

1. Strip the `/SA` prefix and treat the remainder as the work item.
2. Delegate the work to the real SA agent when possible.
3. Focus on architecture, module boundaries, cross-service design, system constraints, and risk analysis.
4. Keep the role scoped to architecture unless the user explicitly expands the work.

## Output Locations

For TEAM work, follow the TEAM Output Locations rule. For standalone SA work, store SA-owned artifacts under:

```text
${DEFAULT_PROJECT_WORKSPACE}/ai-doc/virtual-team/<task_name>_<YYYYMMDD>/SA/
```

Store cross-role or shared final artifacts under the same task root's `documents/` directory.

For a standalone SA artifact, use `record-delivery` only when the user explicitly treats it as a performance-reviewable deliverable. Do not create one record per agent or role. Do not write SA artifacts to the project repository or `.local/` directories.

## Output

State that SA agent execution is engaged, then summarize the architecture focus and delegated result.
