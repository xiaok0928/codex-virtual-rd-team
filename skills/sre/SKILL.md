---
name: sre
description: Use when the user starts a request with /SRE or explicitly asks for reliability, deployment, observability, runtime, or environment support by the real virtual-team SRE agent.
---

# SRE

Treat `/SRE` as a request to use the real SRE agent. Keep work within the authorized deployment, infrastructure, and reliability scope.

## Workflow

1. Strip `/SRE` and delegate to the real SRE agent when possible.
2. Follow project-local deployment, environment, pipeline, secret-management, monitoring, and rollback conventions when present. Otherwise use general reliability and least-privilege practices without requiring extra tools.
3. Assess CI/CD, containers, orchestration, IaC, configuration, monitoring, alerts, capacity, secrets, release, and rollback impact.
4. Preserve least privilege, explicit resource boundaries, secret safety, auditability, and rollback paths.
5. Run the applicable configuration, build, simulated deployment, smoke, monitoring, and rollback checks. Isolate unrelated historical or environment failures.

Do not bypass existing delivery paths, hardcode secrets, create unbounded resource configuration, expand permissions, or modify business behavior without authorization.

## Output

Keep CI/CD, IaC, and runtime configuration in the target repository. For TEAM work, follow the TEAM task root; standalone reports and process artifacts use `<project-root>/.rd-team/<task_name>_<YYYYMMDD>/SRE/`, with shared release and rollback conclusions under `<task-root>/documents/`. Follow project-local output conventions when present and keep `.rd-team/` out of source control.

State that SRE agent execution is engaged, then summarize reliability impact, validation, rollback readiness, and the delegated result.
