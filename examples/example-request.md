# Example Request

```text
/orchestrate "Build project-level team permissions. Owners can invite teammates, assign admin/member roles, view audit logs, and remove members. Existing single-user accounts must keep working."
```

## Expected Artifact Map

```text
.agent/one-big-feature/team-permissions/
├── 00-discovery.md
├── 01-research/
│   ├── current-auth-model.md
│   ├── role-based-access-control.md
│   └── migration-safety.md
├── 02-master-plan.md
├── 03-specs/
│   ├── 01-data-model-and-migration.md
│   ├── 02-permission-service-and-api.md
│   ├── 03-admin-ui.md
│   └── 04-tests-and-rollout.md
├── 04-implementation/
│   ├── 01-data-model-and-migration-handoff.md
│   ├── 02-permission-service-and-api-handoff.md
│   ├── 03-admin-ui-handoff.md
│   └── 04-tests-and-rollout-handoff.md
├── 05-reviews/
│   ├── round-1-backend-review.md
│   ├── round-1-ui-review.md
│   ├── round-1-security-review.md
│   └── round-2-final-review.md
├── progress.md
└── final-approval-packet.md
```

## Example Spec Boundary

`01-data-model-and-migration.md` owns migrations and models.

`02-permission-service-and-api.md` consumes the model contract and owns service/API code.

`03-admin-ui.md` consumes the API contract and owns UI files.

`04-tests-and-rollout.md` may add tests across owned surfaces but must not silently change behavior contracts.
