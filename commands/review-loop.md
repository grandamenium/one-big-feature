# /review-loop

Use after `/implement`.

Input:

- integrated feature branch or PR
- `03-specs/`
- `04-implementation/`
- current test results

Output:

- review reports in `05-reviews/`
- fixes applied through writer/fix agents
- `final-approval-packet.md`

## Procedure

1. Confirm the integrated branch or PR is ready for review.
2. Deploy reviewer agents by risk area or implemented PR/spec.
3. Every reviewer must review the full integrated feature, not only an isolated shard.
4. Require reviewers to inspect adjacent contracted specs.
5. Collect scores and findings.
6. If any review is below pass threshold, send findings to writer/fix agents.
7. Re-run affected tests and integration checks.
8. Re-review until all review scores pass or the human accepts residual risk.
9. Write `final-approval-packet.md` using `templates/final-approval-packet.md`.
10. Ask the human for approval before merge, deploy, or irreversible action.

## Reviewer Prompt

```text
You are a reviewer for a One Big Feature integrated PR.

Review the full integrated feature, not only one shard.

Read:
- 00-discovery.md
- 02-master-plan.md
- all files in 03-specs/
- all handoffs in 04-implementation/
- the integrated diff or PR

Focus on:
- correctness
- adjacent-spec contract compatibility
- missing tests
- broken user flows
- security/privacy risks
- migrations and rollback
- performance
- maintainability
- scope drift
- docs and rollout gaps

Return a review report with:
- score from 1 to 5
- pass/fail recommendation
- actionable findings with file references
- reproduction steps where relevant
- required validation
- adjacent-spec synthesis notes

A 5 means you would approve the PR after the listed validation.
```

## Rating Standard

| Score | Meaning |
| --- | --- |
| 5 | Ready for human approval after listed validation |
| 4 | Mostly ready, small issues or test gaps |
| 3 | Significant issues remain |
| 2 | Major correctness or integration risk |
| 1 | Not coherent or not reviewable |

## Loop Rule

The loop continues until:

- every reviewer returns 5, or
- the human explicitly accepts documented residual risk.

Silence is not approval.
