---
name: sre
description: Use when the user starts a request with /SRE or explicitly asks for reliability, deployment, observability, runtime, or environment support by the real virtual-team SRE agent.
---

# SRE

Use this skill when the user starts a request with `/SRE` or explicitly asks for site reliability support.

## Agent Delegation

Treat `/SRE` as a request to use the real virtual-team SRE agent. If multi-agent tools are available, delegate to the current runtime's SRE agent type, such as `sre` after agent reload or `ops-engineer` in older loaded sessions. The main agent coordinates and summarizes; it should only handle SRE work locally when agent delegation is unavailable, and must say so.

## Workflow

1. Strip the `/SRE` prefix and treat the remainder as the work item.
2. Delegate the work to the real SRE agent when possible.
3. Focus on deployment, observability, runtime reliability, environment concerns, release risk, monitoring, rollback, and operational readiness.
4. Keep the role scoped to SRE and reliability work unless the user explicitly expands the work.

## Output Locations

For TEAM work, follow the TEAM Output Locations rule. SRE-owned artifacts go under `SRE/`, and cross-role or shared final artifacts go under `documents/`.

When working inside a project repository, use:

```text
.rd-team/SRE/<task_name>_<YYYYMMDD>/
```

Keep `.rd-team/` out of source control. For Git projects without an existing ignore rule, prefer the local `.git/info/exclude` unless the project explicitly wants a shared `.gitignore` rule.

If the project defines local output or delivery-record conventions, follow them. Otherwise, do not require an additional delivery record.

## Output

State that SRE agent execution is engaged, then summarize reliability, runtime, release focus, and delegated result.
