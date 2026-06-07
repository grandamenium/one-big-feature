# /plan

Use after `/orchestrate`.

Input:

- `00-discovery.md`
- all files in `01-research/`
- current repo state

Output:

- `02-master-plan.md`

## Procedure

1. Read `00-discovery.md`, all research files, and `progress.md`.
2. Deploy one planning subagent if the harness supports subagents. If not, perform the planner role in the current session.
3. The planner must produce one master plan, not code.
4. Review the planner output as orchestrator. Tighten vague ownership, missing tests, unbounded scope, unsafe rollout assumptions, or contract gaps.
5. Save the final plan as `02-master-plan.md` using `templates/master-plan.md`.
6. Update `progress.md`.

## Planner Requirements

The master plan must include:

- feature summary
- non-goals
- current architecture findings
- proposed architecture
- shard/spec list
- dependency graph
- file ownership boundaries
- shared contracts
- migration/data concerns
- testing plan
- rollout plan
- risks and mitigations
- human approval gates

## Planner Prompt

```text
You are the planner for one self-contained production feature.

Read:
- 00-discovery.md
- every file in 01-research/
- relevant repo docs and source files

Produce 02-master-plan.md. Do not write application code.

Your plan must define feature summary, non-goals, architecture, shard list, file ownership, cross-spec contracts, dependency order, validation plan, rollout safety, and open risks.

Each shard must be precise enough to become a self-contained implementation spec for one writer agent.
```

## Quality Gate

The plan is not done until:

- every spec has clear boundaries
- every shared contract has one owner
- every dependency is ordered
- every user-facing behavior has validation
- every migration or data risk has a safety plan
- merge/deploy approval is explicitly gated
