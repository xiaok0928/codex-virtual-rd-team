---
name: team
description: Use when the user wants the full virtual R&D team to collaborate on a request using the real PM, SA, TPM, UI, BE, FE, QA, and SRE agents.
---

# Team

## Workspace configuration

Read `~/.codex/AGENTS.md` first, resolve `DEFAULT_PROJECT_WORKSPACE`, and normalize it to an absolute path without a trailing slash. Use it as the default delivery root for `ai-doc`, virtual-team, planning, and delivery outputs. A delivery workspace explicitly supplied by the user overrides it for the current request. Do not infer the affected source repository from this path.

Use for `TEAM` or `/team` requests.

## Agent Delegation

Treat `TEAM` as a request to coordinate the real virtual R&D team agents, not as a request for the main agent to simulate roles.

Real team roles:

- PM: `pm`
- UI: `ui`
- SA: `sa`
- TPM: `tpm` after reload, or `tl` in older loaded sessions
- BE: `be` after reload, or `backend-developer` in older loaded sessions
- FE: `fe` after reload, or `frontend-developer` in older loaded sessions
- QA: `qa` after reload, or `qa-engineer` in older loaded sessions
- SRE: `sre` after reload, or `ops-engineer` in older loaded sessions

The main agent coordinates the team, passes shared context, enforces checkpoints, tracks parallel work, resolves handoff order, integrates results, and summarizes. If multi-agent delegation is unavailable, clearly state the fallback before doing any role work locally.

## Workflow

1. Treat the request after `/team` as the work item.
2. Bring up real PM, SA, TPM, UI, BE, FE, QA, and SRE agents for visible initial alignment. Each role states its initial reading of the request.
3. During initial alignment, UI must participate and give input on visual consistency, interaction complexity, page layout, design assets, cross-platform adaptation, implementation feasibility, experience risks, and design effort risks.
4. Use the initial statements to surface gaps, disagreements, and shared assumptions until the team reaches a common understanding.
5. PM produces the PRD for user confirmation.
6. After PM is confirmed, run UI and SA in parallel when both are relevant:
   - UI produces visual direction, page design plan, and UI deliverable plan for user confirmation when the work has a user interface.
   - SA produces system boundary and solution constraints for user confirmation.
   - UI and SA may discuss cross-impact issues, but neither should block the other unless design direction and system boundary have a real dependency.
7. After UI is confirmed or skipped, and SA is confirmed, TPM decomposes work and assigns ownership for user confirmation. TPM must include UI work, deliverables, dependencies, and timing when UI is involved.
8. After TPM is confirmed, enter execution:
   - For complex multi-stage execution, activate `planning-with-files` as a virtual-team-only workflow and store its files under the current virtual-team task directory.
   - Distribute work to real UI, BE, FE, QA, and SRE agents as needed, and run independent role work in parallel by default.
   - UI produces current-version UI deliverables under `<task-root>/versions/<version>/UI/`, including visual guidelines, HTML page designs, sliced assets, specs, and a Markdown file describing every output file's purpose and key points.
   - UI submits completed deliverables to PM for confirmation. PM reviews against the PRD, current-version scope, business goals, and acceptance criteria.
   - If PM requests changes, UI updates relevant files and resubmits them. Repeat until UI and PM agree.
   - After PM confirms UI deliverables, ask the user to confirm UI deliverables before moving forward.
   - After user confirmation, FE and UI align on the design contract before FE implements UI pages.
   - If the task involves frontend/backend integration, BE and FE align on the API contract before integration implementation.
   - BE and FE may start parallel development only after both sides confirm the API contract is correct.
   - QA and SRE may proceed in parallel with preparation that does not depend on unfinished UI/BE/FE implementation.
   - QA writes test cases and leads test case review with relevant team members. QA cases should use both PM PRD and confirmed UI deliverables when the work has a user interface.
   - If PM-confirmed UI files change later, UI clearly marks changed points and notifies FE and QA.
   - After BE and FE complete development, QA tests against agreed test cases and outputs test results.
   - BE and FE fix bugs according to QA test results, then return fixes for QA retesting.
   - If BE, FE, QA, UI, or other roles disagree about a test case, PM and SA must participate, resolve the disagreement, and drive the team to a shared decision before the next step continues.
   - Repeat the test, fix, and retest loop until all agreed test cases pass.
   - After testing fully passes, QA outputs the final test report.
   - The main agent tracks role progress, keeps each role's output visible without collapsing it into a summary, merges results, resolves conflicts, and performs final integration validation.
9. If the user later targets a single role directly, use that real role agent instead.

## Guardrails

- PM and TPM checkpoints are sequential.
- After PM confirmation, UI and SA checkpoints run in parallel when both are relevant.
- TPM starts only after UI is confirmed or skipped, and SA is confirmed.
- Execution after TPM confirmation is parallel by default.
- Use serial or staged execution only when roles have a clear hard dependency, must modify the same files/modules, or the required contract cannot be safely inferred.
- Do not let FE begin UI page implementation before PM confirms UI deliverables, the user confirms UI deliverables, and FE/UI confirm the design contract.
- Do not let BE and FE begin integration implementation before their shared API contract is confirmed.
- Do not treat QA test cases as final until relevant team members have reviewed and agreed on them.
- Do not finish the TEAM workflow before QA has tested against agreed cases, BE/FE have fixed reported bugs, all agreed cases pass, and QA has produced the final test report.

## Output Locations

Use one task root for every virtual-team artifact:

```text
${DEFAULT_PROJECT_WORKSPACE}/ai-doc/virtual-team/<task_name>_<YYYYMMDD>/
```

Role-owned execution artifacts:

```text
<task-root>/<ROLE>/
```

Product-version deliverables:

```text
<task-root>/versions/<version>/<ROLE>/
```

Shared final artifacts and cross-role records:

```text
<task-root>/documents/
```

Virtual-team planning files when eligible:

```text
<task-root>/planning-with-files/task_plan.md
<task-root>/planning-with-files/findings.md
<task-root>/planning-with-files/progress.md
```

After eligible virtual-team implementation is complete and QA or final validation has passed, invoke `record-delivery` exactly once for the requirement. Do not create one record per PM, UI, SA, TPM, BE, FE, QA, or SRE role; let `record-delivery` own the location, deduplication, history, validation evidence, and useful role contribution summary.

Role folder names are `PM`, `UI`, `SA`, `TPM`, `BE`, `FE`, `QA`, and `SRE`.

Do not write virtual-team artifacts to project repositories, product roots, Codex session directories, or any `.local/` directory. The default project workspace `ai-doc` tree is authoritative even when the affected code repository lives elsewhere.

Before delegation, the main coordinator must create the canonical task root and confirm it is writable. If a role sandbox cannot write there, the role returns its artifact to the coordinator, which writes it to the canonical path; never fall back to another output directory.

## Output

State that the real virtual team is engaged, surface each role's output in order, and pause at PM, UI when applicable, SA, and TPM checkpoints for user confirmation before moving forward.
