# Issue #1 extraction map

Baseline: Relay `main` `5dc67c27904cede5d1c9db53104cd7bb6ebc07e7`; Relay architecture audit #48. This repository has no Relay runtime dependency.

| Relay source | Decision | Reason |
| --- | --- | --- |
| `src/factory/agents/planner.ts`, `context-selection.ts`, `project-context.ts`, `repository-context.ts`, `orchestrator.ts` | Port with a Factory advisory artifact name | Coherent Planner, context, and identity slice; Node and Zod only |
| `src/orchestration/contracts.ts` | Port | Planner schema and response identity validation dependency; broader role schemas retained unchanged to avoid a risky rewrite |
| `scripts/prepare-planner-handoff.ts`, `run-api-planner.ts` | Port and adapt policy path | Explicit preview/live boundary and source/test coverage |
| `.agents/relay-orchestration-policy.json` | Adapt as `config/factory-policy.json` | Planner model and effort gate |
| Focused `tests/orchestration/{contracts,factory-*,prepare-planner-handoff,run-api-planner}.test.ts` | Port | Offline regression coverage for context, paths, identities, authorization, advisory handoff, and provider failure |
| `src/orchestration/{checkpoint*,file-attempt-reservation,planner-handoff,policy*,reconcile,recovery,simulate,state}.ts`, `scripts/promote-orchestration-policy.ts` | Defer | Reservation, policy promotion, recovery, and dispatch machinery are not required by this advisory slice |
| Issue #47 local browser UI and launcher | Unmerged reference only | Frozen branch; no dependency in this extraction |
| Relay application source, migrations, database guards, workers, outreach, product CI | Keep in Relay | Application ownership and safety boundaries |

## Subsequent Relay cleanup, separate issue and review

Recheck live Relay imports and consumers at the cleanup commit. Reconcile `AGENTS.md`, `.agents/skills/relay-*`, `.claude/skills/relay-*`, policy docs, tests, and CI before removing Factory-only copies and the three scripts (`prepare-planner-handoff.ts`, `run-api-planner.ts`, `promote-orchestration-policy.ts`). Preserve Relay product code, database guards, outreach protections, `npm run verify`, and exact-head CI. Review the cleanup diff and verify Relay independently. Preserve Issue #47's branch and reviewed commit; do not merge it into cleanup.
