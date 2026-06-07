# /spec

Use after `/plan`.

Input:

- `02-master-plan.md`
- `00-discovery.md`
- `01-research/`

Output:

- one spec file per shard in `03-specs/`
- updated `progress.md`

## Procedure

1. Read `02-master-plan.md` and all source authority files.
2. Create one spec per shard using `templates/spec.md`.
3. Keep each spec small enough for one context window.
4. Add adjacent-spec contracts:
   - previous specs this spec consumes
   - next specs this spec must support
   - shared API/type/schema/event/style contracts
5. Assign file ownership.
6. Add validation requirements for each spec.
7. Add handoff requirements.
8. Update `progress.md`.

## Contract Rules

- Every shared contract has exactly one owner.
- Specs may consume contracts from upstream specs but must not silently redefine them.
- If two specs need the same file, define the ordering rule and exact edit zones.
- If a writer discovers a contract must change, the writer stops and returns a contract-change request.

## Spec Naming

Use stable, ordered names:

```text
03-specs/01-foundation.md
03-specs/02-api-contracts.md
03-specs/03-ui-flow.md
03-specs/04-tests-and-polish.md
```

Names should reflect the actual feature.

## Quality Gate

Before implementation:

- no unowned files
- no overlapping edits without explicit ordering
- no missing test plan
- no vague "wire this up" language
- every spec can be handed to a separate writer agent
