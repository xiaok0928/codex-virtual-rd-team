---
name: qa
description: Use when the user starts a request with /QA or explicitly asks for quality validation by the real virtual-team QA agent.
---

# QA

## Workspace configuration

Read `~/.codex/AGENTS.md` first, resolve `DEFAULT_PROJECT_WORKSPACE`, and normalize it to an absolute path without a trailing slash. Use it as the default delivery root for `ai-doc`, virtual-team, planning, and delivery outputs. A delivery workspace explicitly supplied by the user overrides it for the current request. Do not infer the affected source repository from this path.

Use this skill when the user starts a request with `/QA` or explicitly asks for quality validation.

## Agent Delegation

Treat `/QA` as a request to use the real virtual-team QA agent. If multi-agent tools are available, delegate to the current runtime's QA agent type, such as `qa` after agent reload or `qa-engineer` in older loaded sessions. The main agent coordinates and summarizes; it should only handle QA work locally when agent delegation is unavailable, and must say so.

## Workflow

1. Strip the `/QA` prefix and treat the remainder as the work item.
2. Delegate the work to the real QA agent when possible.
3. Focus on test design, boundary checks, validation strategy, test execution, bug reporting, and retesting.
4. Keep the role scoped to QA unless the user explicitly expands the work.

## Output Locations

For TEAM work, follow the TEAM Output Locations rule. For standalone QA work, store test cases, test plans, and execution notes under:

```text
${DEFAULT_PROJECT_WORKSPACE}/ai-doc/virtual-team/<task_name>_<YYYYMMDD>/QA/
```

Store final test reports, bug lists, acceptance records, and cross-role quality summaries under the same task root's `documents/` directory.

For a standalone QA artifact, use `record-delivery` only when the user explicitly treats it as a performance-reviewable deliverable. Do not create one record per agent or role. Do not write QA artifacts to the project repository or `.local/` directories.

## Output

State that QA agent execution is engaged, then summarize the testing focus and delegated result.
