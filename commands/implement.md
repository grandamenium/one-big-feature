# /implement

Use after `/spec`.

Input:

- all files in `03-specs/`
- `02-master-plan.md`
- `progress.md`

Output:

- implemented branches/worktrees
- writer handoffs in `04-implementation/`
- updated `progress.md`

## Procedure

1. Read all specs and the dependency graph.
2. Decide parallel or sequential execution:
   - parallel only for specs with no dependency or file overlap
   - sequential for migrations, shared contracts, or overlapping files
3. Create isolated branches or git worktrees for writer agents.
4. Deploy one writer per ready spec.
5. Give each writer only its assigned spec plus the shared authority files.
6. Require tests and a handoff.
7. Integrate writer work into the main integration branch only after checking:
   - file ownership
   - contract compatibility
   - test results
   - git conflicts
   - uncommitted changes
8. Update `progress.md`.

## Writer Prompt

```text
You are a writer agent for one One Big Feature spec.

Read:
- your assigned spec in 03-specs/
- 02-master-plan.md
- 00-discovery.md
- progress.md

Work only in your assigned branch or worktree.

Rules:
- edit only owned files
- do not modify adjacent specs' owned files
- preserve consumed contracts
- if a contract must change, stop and return a contract-change request
- add or update tests
- run the validation listed in your spec
- commit your work if the environment permits

Return a handoff in 04-implementation/<spec-name>-handoff.md with:
- branch/worktree
- files changed
- behavior implemented
- tests run and results
- screenshots/traces for UI work
- contract changes or confirmations
- known risks
- cleanup notes
```

## Integration Gate

Do not proceed to `/review-loop` until:

- all required specs are implemented
- integration branch contains the combined feature
- conflict checks are clean
- expected tests have been run or explicitly documented as blocked
- `04-implementation/` contains writer handoffs
