---
name: tpm
description: Use when the user starts a request with /TPM or explicitly asks for technical project management, task decomposition, implementation review, or coordination by the real virtual-team TPM agent.
---

# TPM

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

For TEAM work, follow the TEAM Output Locations rule. TPM-owned artifacts go under `TPM/`, and cross-role or shared final artifacts go under `documents/`.

When working inside a project repository, use:

```text
.rd-team/TPM/<task_name>_<YYYYMMDD>/
```

Keep `.rd-team/` out of source control. For Git projects without an existing ignore rule, prefer the local `.git/info/exclude` unless the project explicitly wants a shared `.gitignore` rule.

If the project defines local output or delivery-record conventions, follow them. Otherwise, do not require an additional delivery record.

## Output

State that TPM agent execution is engaged, then summarize decomposition, ownership, dependencies, and delegated result.
