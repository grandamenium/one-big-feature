# Spec <N>: <Spec Name>

**Status**: Ready
**Depends on**: <specs or none>
**Can run in parallel with**: <specs or none>

## Objective

<What this spec builds.>

## Context

<How this spec fits the full feature.>

## Owned Files

These files may be edited by this spec:

- `<path>` - <purpose>

## Read-Only Files

These files may be read but not edited:

- `<path>` - <why>

## Consumed Contracts

| Contract | Provider | How this spec uses it |
| --- | --- | --- |
| <Contract> | <Spec> | <Usage> |

## Provided Contracts

| Contract | Consumers | Shape |
| --- | --- | --- |
| <Contract> | <Specs> | <API/type/schema/event/style> |

## Implementation Steps

1. <Step>
2. <Step>
3. <Step>

## Validation

- [ ] Unit:
- [ ] Integration:
- [ ] Browser/UI:
- [ ] Build/type/lint:
- [ ] Other:

## Acceptance Criteria

- [ ] <Criterion>

## Handoff Requirements

Writer must create:

```text
04-implementation/spec-<N>-<name>-handoff.md
```

Include changed files, tests, risks, contract confirmations/changes, screenshots/traces for UI work, and cleanup notes.

## Stop Conditions

Stop and ask the orchestrator if:

- you need to edit unowned files
- a consumed contract is wrong
- a provided contract must change
- required credentials or external approvals are missing
- validation cannot run
