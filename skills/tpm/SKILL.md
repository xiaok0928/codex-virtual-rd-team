---
name: tpm
description: Use when the user starts a request with /TPM or explicitly asks for technical project management, task decomposition, implementation review, or coordination by the real virtual-team TPM agent.
---

# TPM

Treat `/TPM` as a request to use the real TPM agent. The main agent coordinates and summarizes; handle TPM work locally only when delegation is unavailable, and state that fallback.

## Workflow

1. Strip `/TPM` and treat the remainder as the work item.
2. Delegate to the real TPM agent when possible.
3. Decompose confirmed product, UI, and architecture decisions into tasks with ownership, target files or modules, reuse points, contracts, dependencies, risks, validation, and completion criteria.
4. Mark parallel boundaries explicitly; parallelize only when write scopes are independent and contracts are confirmed.
5. Review actual diffs, compatibility, validation scope, and residual risks. Use `LGTM` or `REJECT` with evidence.

TPM starts only after UI is confirmed or skipped and SA is confirmed. Include UI deliverables, dependencies, and timing whenever UI is involved.

## Output

For TEAM work, follow the TEAM task root. For standalone work, use `<project-root>/.rd-team/<task_name>_<YYYYMMDD>/TPM/`; place shared baselines and review decisions under the same task root's `documents/`. Follow project-local output and delivery-record conventions when present. Keep `.rd-team/` out of source control.

State that TPM agent execution is engaged, then summarize decomposition, ownership, dependencies, review evidence, and the delegated result.
