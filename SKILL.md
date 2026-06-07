---
name: one-big-feature
description: Run a production-quality multi-agent development loop for one substantial feature. Use when the user asks for /orchestrate, /plan, /spec, /implement, /review-loop, one big feature, or wants an orchestrator agent to coordinate discovery, planning, sharded implementation, integrated review, validation, fixes, and a final human approval gate.
triggers:
  - orchestrate
  - plan
  - spec
  - implement
  - review-loop
  - one big feature
  - big feature
  - multi-agent feature
external_calls: []
---

# One Big Feature

Use this skill as the main/orchestrator agent when building one substantial feature to production quality with subagents.

The core pattern:

```text
/orchestrate -> /plan -> /spec -> /implement -> /review-loop -> human approval
```

The main agent never stops owning the outcome. Subagents do bounded work; the orchestrator owns context, contracts, progress, integration, review synthesis, risk, and final communication.

## When To Use

Use for feature work large enough to need discovery, planning, sharding, implementation, review, and validation.

Do not use for a small bug fix unless the fix crosses multiple modules or has serious production risk.

## Required Folder

Create one durable folder inside the target codebase:

```text
.agent/one-big-feature/<feature-slug>/
```

Keep every artifact in that folder unless the repo has an established equivalent.

Required artifacts:

```text
00-discovery.md
01-research/
02-master-plan.md
03-specs/
04-implementation/
05-reviews/
progress.md
final-approval-packet.md
```

## Operating Rules

- Stay the main owner of scope, context, risk, progress, and final human communication.
- Use subagents only for bounded roles: researcher, planner, spec writer, implementation writer, reviewer, and targeted fixer.
- Keep every subagent prompt self-contained. Include repo context, feature goal, relevant artifact paths, constraints, ownership, expected output, validation requirements, and stop conditions.
- Prefer isolated git worktrees or branches for writer agents. If the harness cannot do worktrees, use clearly named branches and non-overlapping file ownership.
- Never let two writer agents own the same file without an explicit contract and ordering rule.
- Treat tests, review, and integration as gates, not decoration.
- Keep `progress.md` current enough for a new context window to resume.
- Ask for human approval before merge, production deployment, data deletion, spending money, external communication, or any irreversible action.

## Slash Phases

### 1. `/orchestrate`

Read `commands/orchestrate.md`.

Goal: interrogate the feature request, inspect the codebase, gather context, perform targeted research, and write durable discovery and research files.

The output must be specific enough that a planner can create a production implementation plan without guessing.

### 2. `/plan`

Read `commands/plan.md`.

Goal: deploy a planner subagent to synthesize discovery and research into one master implementation plan.

The master plan must include:

- feature summary and non-goals
- architecture approach
- shard list
- dependency order
- file ownership strategy
- cross-spec contracts
- test strategy
- rollout and approval gates

### 3. `/spec`

Read `commands/spec.md`.

Goal: split the master plan into spec documents, each small enough for one context window.

Every spec must define:

- objective
- owned files
- files it may read but not edit
- provided contracts
- consumed contracts
- adjacent specs
- implementation steps
- validation requirements
- handoff requirements

### 4. `/implement`

Read `commands/implement.md`.

Goal: deploy writer agents against specs in parallel or sequence, respecting dependency and file-ownership boundaries.

Each writer must return a handoff with:

- files changed
- behavior implemented
- tests run and results
- contract changes
- risks
- screenshots or traces for UI work
- branch/worktree cleanup notes

### 5. `/review-loop`

Read `commands/review-loop.md`.

Goal: deploy review agents against the integrated PR and adjacent contracted specs, collect ratings, fix findings, and repeat until all reviews pass.

Reviewers must review the full integrated feature, not only their own slice.

## Done Criteria

- Discovery and research artifacts exist and reflect the actual repo.
- Master plan defines architecture, dependencies, risks, validation, and rollout.
- Specs define ownership and adjacent-spec contracts.
- Writers implement in isolation and produce handoffs.
- Integration resolves conflicts and preserves contracts.
- Required tests pass or skipped tests are explicitly justified.
- Reviewers return passing ratings, or the human explicitly accepts documented residual risk.
- Final approval packet summarizes the feature, changed files, tests, review scores, risks, and required human decision.
- Human approval is obtained before merge/deploy/irreversible action.

## Subagent Prompt Rules

Planner prompt must include:

```text
You are the planner for one self-contained production feature. Produce a master plan and sharded specs; do not write application code. Include file ownership, contracts between specs, dependency order, worktree or branch instructions, validation plans, conflict checks, rollout risk, and handoff requirements. Make the plan precise enough for independent writer agents to implement without overlapping edits.
```

Writer prompt must include:

```text
You are a writer agent for one spec only. Work only in your assigned branch or worktree. Implement only your owned files and declared contracts. Add or update tests. Run the specified validation. Return a handoff with changed files, tests, risks, contract changes, and cleanup notes. Do not edit unowned files without stopping and asking the orchestrator.
```

Reviewer prompt must include:

```text
You are reviewing the full integrated PR, not only one shard. Evaluate correctness, contract compatibility, security/privacy, UI behavior, tests, rollout safety, performance, maintainability, and whether adjacent specs synthesize into one coherent feature. Return actionable findings with file references, reproduction steps, required validation, and a 1-5 score. A 5 means you would approve this PR after the listed validation.
```

## Human Approval Gate

Before final action, present `final-approval-packet.md` and ask for explicit approval.

Never infer approval from silence.
