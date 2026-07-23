---
name: team
description: Use when the user wants the full virtual R&D team to collaborate on a request using the real PM, SA, TPM, UI, BE, FE, QA, and SRE agents.
---

# Team

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
2. Use the `rd-team-routing` skill to establish the team route and one task root, then bring up real PM, SA, TPM, UI, BE, FE, QA, and SRE agents for visible initial alignment. Each role states its initial reading of the request.
3. During initial alignment, UI must participate and give input on visual consistency, interaction complexity, page layout, design assets, cross-platform adaptation, implementation feasibility, experience risks, and design effort risks.
4. Use the initial statements to surface gaps, disagreements, and shared assumptions until the team reaches a common understanding.
5. PM produces the PRD for user confirmation.
6. After PM is confirmed, run UI and SA in parallel when both are relevant:
   - UI produces visual direction, page design plan, and UI deliverable plan for user confirmation when the work has a user interface.
   - SA produces system boundary and solution constraints for user confirmation.
   - UI and SA may discuss cross-impact issues, but neither should block the other unless design direction and system boundary have a real dependency.
7. After UI is confirmed or skipped, and SA is confirmed, TPM decomposes work and assigns ownership for user confirmation. TPM must include UI work, deliverables, dependencies, and timing when UI is involved.
8. After TPM is confirmed, enter execution:
   - For complex multi-stage implementation, use file-based planning under the current task root. Do not require it for planning, consultation, documentation-only, narrow, or ordinary single-agent work.
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

- Before development starts, inspect the target project's `AGENTS.md`, contribution guide, engineering docs, build scripts, test commands, output rules, and other local conventions. Follow them when present; they override the default development and output suggestions in this skill.
- If the project has no local development conventions, do not block the workflow or require additional skills, tools, directories, or planning files. Use the existing codebase patterns and general engineering practices.
- Keep `.rd-team/` out of source control. If a Git project does not already ignore it, prefer adding `.rd-team/` to the local `.git/info/exclude`; modify the tracked `.gitignore` only when the user or project explicitly wants a shared ignore rule.
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

Use one task root unless the target project defines another output convention:

```text
<project-root>/.rd-team/<task_name>_<YYYYMMDD>/
```

Role-owned execution artifacts:

```text
<task-root>/<ROLE>/
```

Product-version deliverables:

```text
<task-root>/versions/<version>/<ROLE>/
```

Shared final artifacts:

```text
<task-root>/documents/
```

File-based planning when eligible:

```text
<task-root>/planning-with-files/
```

If the project defines local output, planning, or delivery-record conventions, follow them. Otherwise, the TEAM workflow does not require extra project-specific directories or records beyond the role outputs needed for the task.

Role folder names are `PM`, `UI`, `SA`, `TPM`, `BE`, `FE`, `QA`, and `SRE`.

## Output

State that the real virtual team is engaged, surface each role's output in order, and pause at PM, UI when applicable, SA, and TPM checkpoints for user confirmation before moving forward.
