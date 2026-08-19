# R&D Team Agents

## Workspace configuration

Read `~/.codex/AGENTS.md` first, resolve `DEFAULT_PROJECT_WORKSPACE`, and normalize it to an absolute path without a trailing slash. Use it as the default delivery root for `ai-doc`, virtual-team, planning, and delivery outputs. A delivery workspace explicitly supplied by the user overrides it for the current request. Do not infer the affected source repository from this path.

This directory contains the real PM, UI, SA, TPM, BE, FE, QA, and SRE Agent role definitions. Triggering, routing, and shared workflow rules live under `~/.codex/skills/`.

## Roles

- `pm.toml`: product scope, PRD, acceptance criteria, risk and product decisions.
- `ui.toml`: visual direction, page design, assets, specs, UI confirmation and FE handoff.
- `sa.toml`: system boundaries, architecture constraints, data flow and technical risks.
- `tpm.toml`: task decomposition, ownership, dependencies, sequencing and code review gates.
- `be.toml`: backend APIs, services, persistence, performance, concurrency and backend tests.
- `fe.toml`: frontend pages, components, client state, API integration and frontend validation.
- `qa.toml`: test cases, review, execution, defects, retesting and final quality reporting.
- `sre.toml`: delivery pipelines, infrastructure, observability, release, rollback and reliability.

`routing.toml` is intentionally absent. Routing is a workflow, not an Agent role, and is implemented by the `rd-team-routing` Skill.

## Skill mapping

- Use `team` for the full team.
- Use `bf` for the small BE/FE path.
- Use `rd-team-routing` to select the smallest safe role set and enforce contract gates.
- Apply global and applicable project-level `AGENTS.md` rules for programming, tests, scripts, build, deployment configuration, and reviews.
- Use `aitool-middleware` for external middleware access, `maintain-project-docs` for durable project documentation, and `record-delivery` for the single requirement-level delivery record.
- Use `planning-with-files` only inside an active, confirmed, complex multi-stage virtual-team implementation.
- Do not reference retired aliases or optional skills that are not currently available.

## Shared workflow

1. PM confirms product scope and acceptance criteria when needed.
2. UI and SA may run in parallel after PM confirmation.
3. TPM starts after UI is confirmed or skipped and SA is confirmed.
4. UI deliverables require PM review and user confirmation before FE page implementation.
5. BE and FE confirm the API contract before integration implementation.
6. QA cases are reviewed by relevant roles; PM and SA resolve disputed expectations.
7. Test, fix and retest until agreed scope passes or an unrelated/environment failure is isolated.

## Output locations

Use one canonical task root:

```text
${DEFAULT_PROJECT_WORKSPACE}/ai-doc/virtual-team/<task_name>_<YYYYMMDD>/
```

Role output:

```text
<task-root>/<ROLE>/
```

Version output:

```text
<task-root>/versions/<version>/<ROLE>/
```

Shared output and planning:

```text
<task-root>/documents/
<task-root>/planning-with-files/
```

The main coordinator invokes `record-delivery` once when the shared requirement or an explicitly performance-reviewable standalone role artifact is eligible. Individual roles do not write separate delivery records.

Do not write virtual-team process or document artifacts to project repositories, product roots, Codex session directories, or `.local/` directories. Source, tests and deployment configuration remain in their actual project repositories.

The main coordinator creates the canonical task root before delegation. If a role sandbox cannot write there, the role returns its complete artifact to the coordinator, which persists it in the canonical location.

## Validation

Require validation proportional to the changed scope. All directly affected checks must pass. Unrelated historical code or environment failures must be isolated and reported rather than fixed by expanding the task. Never claim unexecuted or blocked validation passed.

## Migration

Back up and restore both directories:

```text
~/.codex/skills/
~/.codex/agents/
```
