---
name: tpm
description: Use when the user starts a request with /TPM or explicitly asks for technical project management, task decomposition, implementation review, or coordination by the real virtual-team TPM agent.
---

# TPM

## Workspace configuration

Read `~/.codex/AGENTS.md` first, resolve `DEFAULT_PROJECT_WORKSPACE`, and normalize it to an absolute path without a trailing slash. Use it as the default delivery root for `ai-doc`, virtual-team, planning, and delivery outputs. A delivery workspace explicitly supplied by the user overrides it for the current request. Do not infer the affected source repository from this path.

Use this skill when the user starts a request with `/TPM` or explicitly asks for technical project management support.

## Agent Delegation

Treat `/TPM` as a request to use the real virtual-team TPM agent. If multi-agent tools are available, delegate to the current runtime's TPM agent type, such as `tpm` after agent reload or `tl` in older loaded sessions. The main agent coordinates and summarizes; it should only handle TPM work locally when agent delegation is unavailable, and must say so.

## Workflow

1. Strip the `/TPM` prefix and treat the remainder as the work item.
2. Delegate the work to the real TPM agent when possible.
3. Focus on task decomposition, ownership assignment, implementation review, technical coordination, dependency tracking, and execution sequencing.
4. Include UI work, deliverables, dependencies, and timing when UI is involved.
5. Keep the role scoped to technical project management unless the user explicitly expands the work.

## Output Locations

For TEAM work, follow the TEAM Output Locations rule. For standalone TPM work, store TPM-owned artifacts under:

```text
${DEFAULT_PROJECT_WORKSPACE}/ai-doc/virtual-team/<task_name>_<YYYYMMDD>/TPM/
```

Store cross-role or shared final artifacts under the same task root's `documents/` directory.

For a standalone TPM artifact, use `record-delivery` only when the user explicitly treats it as a performance-reviewable deliverable. Do not create one record per agent or role. Do not write TPM artifacts to the project repository or `.local/` directories.

## Output

State that TPM agent execution is engaged, then summarize decomposition, ownership, dependencies, and delegated result.
