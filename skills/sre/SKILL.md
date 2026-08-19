---
name: sre
description: Use when the user starts a request with /SRE or explicitly asks for reliability, deployment, observability, runtime, or environment support by the real virtual-team SRE agent.
---

# SRE

## Workspace configuration

Read `~/.codex/AGENTS.md` first, resolve `DEFAULT_PROJECT_WORKSPACE`, and normalize it to an absolute path without a trailing slash. Use it as the default delivery root for `ai-doc`, virtual-team, planning, and delivery outputs. A delivery workspace explicitly supplied by the user overrides it for the current request. Do not infer the affected source repository from this path.

Use this skill when the user starts a request with `/SRE` or explicitly asks for site reliability support.

## Agent Delegation

Treat `/SRE` as a request to use the real virtual-team SRE agent. If multi-agent tools are available, delegate to the current runtime's SRE agent type, such as `sre` after agent reload or `ops-engineer` in older loaded sessions. The main agent coordinates and summarizes; it should only handle SRE work locally when agent delegation is unavailable, and must say so.

## Workflow

1. Strip the `/SRE` prefix and treat the remainder as the work item.
2. Delegate the work to the real SRE agent when possible.
3. Focus on deployment, observability, runtime reliability, environment concerns, release risk, monitoring, rollback, and operational readiness.
4. Keep the role scoped to SRE and reliability work unless the user explicitly expands the work.

## Output Locations

For TEAM work, follow the TEAM Output Locations rule. For standalone SRE work, store SRE-owned artifacts under:

```text
${DEFAULT_PROJECT_WORKSPACE}/ai-doc/virtual-team/<task_name>_<YYYYMMDD>/SRE/
```

Store cross-role or shared final artifacts under the same task root's `documents/` directory.

For a standalone SRE artifact, use `record-delivery` only when the user explicitly treats it as a performance-reviewable deliverable. Do not create one record per agent or role. Do not write SRE artifacts to the project repository or `.local/` directories.

## Output

State that SRE agent execution is engaged, then summarize reliability, runtime, release focus, and delegated result.
