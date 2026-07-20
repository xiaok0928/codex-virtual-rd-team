---
name: qa
description: Use when the user starts a request with /QA or explicitly asks for quality validation by the real virtual-team QA agent.
---

# QA

Use this skill when the user starts a request with `/QA` or explicitly asks for quality validation.

## Agent Delegation

Treat `/QA` as a request to use the real virtual-team QA agent. If multi-agent tools are available, delegate to the current runtime's QA agent type, such as `qa` after agent reload or `qa-engineer` in older loaded sessions. The main agent coordinates and summarizes; it should only handle QA work locally when agent delegation is unavailable, and must say so.

## Workflow

1. Strip the `/QA` prefix and treat the remainder as the work item.
2. Delegate the work to the real QA agent when possible.
3. Focus on test design, boundary checks, validation strategy, test execution, bug reporting, and retesting.
4. Keep the role scoped to QA unless the user explicitly expands the work.

## Output Locations

For TEAM work, follow the TEAM Output Locations rule. QA test cases, test plans, and execution notes go under `QA/`. Final test reports, bug lists, final acceptance records, and cross-role quality summaries go under `documents/`.

When working inside a project repository, use:

```text
.rd-team/QA/<task_name>_<YYYYMMDD>/
```

Keep `.rd-team/` out of source control. For Git projects without an existing ignore rule, prefer the local `.git/info/exclude` unless the project explicitly wants a shared `.gitignore` rule.

If the project defines local output or delivery-record conventions, follow them. Otherwise, do not require an additional delivery record.

## Output

State that QA agent execution is engaged, then summarize the testing focus and delegated result.
