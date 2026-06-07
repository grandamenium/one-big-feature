# /orchestrate

Use this command first.

Input: the user's feature request.

Output:

- `.agent/one-big-feature/<feature-slug>/00-discovery.md`
- `.agent/one-big-feature/<feature-slug>/01-research/*.md`
- `.agent/one-big-feature/<feature-slug>/progress.md`

## Procedure

1. Create a stable feature slug from the request.
2. Create `.agent/one-big-feature/<feature-slug>/` with `01-research/`, `03-specs/`, `04-implementation/`, and `05-reviews/`.
3. Inspect the repo:
   - `git status`
   - README and contributor docs
   - package/dependency files
   - existing tests
   - relevant source files
   - existing architecture or design docs
4. Ask discovery questions before planning. Prefer specific, decision-forcing questions.
5. Only ask the human for decisions that cannot be resolved by repo inspection or public documentation.
6. Research relevant technical areas. Use primary docs for framework/API facts and the repo's existing patterns for implementation style.
7. Write `00-discovery.md` using `templates/discovery.md`.
8. Write one research file per domain using `templates/research.md`.
9. Write or update `progress.md` using `templates/progress.md`.

## Discovery Checklist

Cover every category that applies:

- product goal
- user flows
- non-goals
- auth and permissions
- data model
- APIs and integrations
- UI surfaces and responsive behavior
- migrations and backwards compatibility
- security and privacy
- performance and scale
- analytics/logging/observability
- rollout strategy
- testing expectations
- deployment/runtime constraints
- human approval gates

## Completeness Gate

Before ending `/orchestrate`, ask:

```text
Could a planner agent read only these discovery and research files and produce a correct implementation plan without guessing?
```

If no, continue asking questions or researching.

## Output Format

End by reporting:

- orchestration folder path
- key decisions recorded
- open human questions, if any
- research files created
- recommended next command: `/plan`
