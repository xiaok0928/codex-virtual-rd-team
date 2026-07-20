# R&D Team Agents

This directory contains the user's real virtual R&D team agent configuration.

Use it together with `~/.codex/skills/`. Skills describe trigger/workflow behavior; these TOML files define the actual role agents and routing rules.

## Roles

- `pm.toml`: PM. Owns PRD, requirement definition, current-version scope, acceptance criteria, risk decisions, and test case dispute resolution.
- `ui.toml`: UI. Owns visual direction, page design, slicing/assets, UI specs, UI handoff docs, PM confirmation, user confirmation, and FE design contract alignment.
- `sa.toml`: SA. Owns system boundary, architecture constraints, service/module boundaries, storage/concurrency risks, and solution guardrails.
- `tpm.toml`: TPM. Owns task decomposition, ownership assignment, dependency tracking, execution sequencing, and technical coordination.
- `be.toml`: BE. Owns backend implementation, APIs, persistence, service logic, performance safeguards, backend tests, and backend validation.
- `fe.toml`: FE. Owns frontend implementation, UI page development from confirmed UI specs, component/state logic, API integration, frontend tests, and build checks.
- `qa.toml`: QA. Owns test cases, test case review, test execution, bug feedback, retesting, and final quality reporting.
- `sre.toml`: SRE. Owns deployment, runtime reliability, observability, rollback, environment concerns, release risk, and operational readiness.
- `routing.toml`: Role selection, TEAM workflow, parallel rules, contract gates, QA loop, and output locations.

## TEAM Workflow

1. Requirement enters through `TEAM` or `/team`.
2. Bring up PM, SA, TPM, UI, BE, FE, QA, and SRE for visible initial alignment.
3. UI participates in requirement alignment and comments on visual consistency, interaction complexity, page layout, design assets, cross-platform adaptation, implementation feasibility, experience risks, and design effort risks.
4. PM produces the PRD, current-version scope, non-goals, deferred items, risks, and acceptance criteria for user confirmation.
5. After PM confirmation, UI and SA run in parallel when both are relevant:
   - UI produces visual direction, page design plan, and UI deliverable plan for user confirmation.
   - SA produces system boundary and solution constraints for user confirmation.
6. TPM starts only after UI is confirmed or skipped, and SA is confirmed. TPM decomposes work, assigns ownership, and includes UI deliverables, dependencies, and timing when UI is involved.
7. After TPM confirmation, execution is parallel by default across UI, BE, FE, QA, and SRE.

## Contract Gates

- UI gate: UI deliverables must be reviewed by PM, updated until PM and UI agree, then confirmed by the user.
- Design contract: after user confirmation, UI and FE align on page structure, component states, interactions, responsive behavior, sliced assets, colors, typography, spacing, empty states, loading states, and error states. FE must not begin UI page implementation before this is confirmed.
- API contract: BE and FE align on route, method, request parameters, response shape, error states, auth/permission needs, and pagination/filter/sort behavior before integration implementation.
- Disputes: PM coordinates UI/FE disputes about product intent or implementation tradeoffs. PM and SA handle disputed QA test cases.

## QA Loop

1. QA writes test cases and leads review with relevant team members.
2. QA cases use PM PRD and confirmed UI deliverables when UI exists.
3. The team must agree on test cases before QA uses them as the execution baseline.
4. After BE/FE development, QA tests and outputs results.
5. BE/FE fix bugs according to QA results.
6. QA retests.
7. Repeat until all agreed cases pass.
8. QA outputs the final test report.

## Output Locations

The following locations are defaults. If the target project defines local documentation, output, naming, or delivery conventions, those project-local rules take priority. If no local convention exists, use only the role outputs needed for the task and do not require extra tooling or records.

Keep `.rd-team/` out of source control. In Git projects that do not already ignore it, prefer adding `.rd-team/` to the local `.git/info/exclude`. Modify a tracked `.gitignore` only when the project explicitly wants to share the ignore rule.

Product-version deliverables:

```text
<product-root>/<YYYYMMDD>_<version>/<ROLE>/
```

Example:

```text
demo/20260707_V0.0.1/UI/
```

Shared final artifacts:

```text
<product-root>/<YYYYMMDD>_<version>/documents/
```

Project-local execution artifacts:

```text
<project-root>/.rd-team/<ROLE>/<task_name>_<YYYYMMDD>/
```

Example:

```text
demo/.rd-team/BE/create_role_20260707/
```

Shared project-local artifacts:

```text
<project-root>/.rd-team/documents/<task_name>_<YYYYMMDD>/
```

Rules:

- Dates use `YYYYMMDD`.
- Product version folders use `<YYYYMMDD>_<version>`, such as `20260707_V0.0.1`.
- Role folders use `PM`, `UI`, `SA`, `TPM`, `BE`, `FE`, `QA`, and `SRE`.
- Each role folder should include `README.md` when multiple files are produced.
- QA final test reports, bug lists, final acceptance records, and cross-role quality summaries go under `documents/`.
- QA test cases, plans, and execution notes stay under `QA/`.
- PM PRD drafts, version scope, acceptance criteria, and product decisions stay under `PM/`; final PRD baselines or cross-role decisions may also go under `documents/`.
- UI visual guidelines, page designs, sliced assets, specs, and handoff notes stay under `UI/`; cross-role UI confirmation records may also go under `documents/`.

## Migration

To migrate this team to another computer, back up and restore both directories:

```text
~/.codex/skills/
~/.codex/agents/
```

The `skills/*/agents/openai.yaml` files are UI-facing skill metadata. The real virtual team agents are in this directory.
