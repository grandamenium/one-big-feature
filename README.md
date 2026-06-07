# One Big Feature Skill

A public, agent-readable workflow for shipping one production-quality feature with an orchestrated fleet of coding agents.

This repo packages the "one big feature" methodology as a reusable skill. It is designed for Claude Code, Codex, Cursor-style agent sessions, and other coding-agent harnesses that can read Markdown instructions, inspect a repo, create files, run tests, and delegate work to subagents.

## What It Does

The skill turns one large feature request into a durable multi-agent workflow:

1. `/orchestrate` - the main agent asks discovery questions, researches the codebase and technical context, and writes the source-of-truth context files.
2. `/plan` - a planning subagent reads those files and produces one master implementation plan.
3. `/spec` - the master plan is split into small spec files, each sized for one context window and connected by explicit contracts.
4. `/implement` - writer agents implement each spec in isolated branches or worktrees, either in parallel or sequence.
5. `/review-loop` - reviewer agents review the integrated PR and adjacent contracted work, rate the feature, and send fixes back through the loop until the work passes.

The main agent stays the orchestrator the whole time. It owns context, risk, sequencing, integration, and the final human approval gate.

## Why This Exists

The failure mode for multi-agent coding is opening five sessions and telling all of them to "help build the app." That creates overlapping edits, duplicated work, contract drift, broken tests, and merge conflicts.

This skill uses a different pattern:

- one orchestrator
- one durable orchestration folder
- one master plan
- spec-sized context windows
- explicit adjacent-spec contracts
- isolated writer work
- integrated review loops
- human approval before merge or deploy

## Install

Clone the repo anywhere your coding agent can read it:

```bash
git clone https://github.com/grandamenium/one-big-feature.git
```

For Claude Code, copy or symlink the skill into your local skills directory:

```bash
mkdir -p ~/.claude/skills
ln -s "$(pwd)/one-big-feature" ~/.claude/skills/one-big-feature
```

For Codex or other harnesses, point the agent at `SKILL.md` and the `commands/` and `templates/` folders.

## Quick Start

From the repo where you want to build the feature:

```text
/orchestrate "Build project-level team permissions with roles, invitations, audit log entries, and admin UI."
```

Then run the remaining phases as the prior phase completes:

```text
/plan
/spec
/implement
/review-loop
```

If your harness does not support slash commands, paste the relevant file from `commands/` into the agent session:

- `commands/orchestrate.md`
- `commands/plan.md`
- `commands/spec.md`
- `commands/implement.md`
- `commands/review-loop.md`

## File Outputs

By default, the skill writes durable artifacts into:

```text
.agent/one-big-feature/<feature-slug>/
```

Expected files:

```text
.agent/one-big-feature/<feature-slug>/
├── 00-discovery.md
├── 01-research/
├── 02-master-plan.md
├── 03-specs/
├── 04-implementation/
├── 05-reviews/
├── progress.md
└── final-approval-packet.md
```

These files are the continuity layer. A fresh context window should be able to resume from them without relying on chat history.

## Safety Rules

- Do not let two writer agents edit the same files unless the spec explicitly says so.
- Prefer isolated git worktrees or branches per writer.
- Require every spec to define owned files, consumed contracts, provided contracts, tests, and done criteria.
- Review the integrated PR, not just isolated diffs.
- Run the tests that match the feature: unit, integration, lint/typecheck/build, browser/UI checks, and live functional checks when relevant.
- Do not merge, deploy, spend money, send external messages, delete data, or take irreversible action without explicit human approval.

## Repo Contents

| Path | Purpose |
| --- | --- |
| `SKILL.md` | Main agent-readable skill instructions |
| `commands/` | Slash-command phase prompts |
| `templates/` | Durable artifact templates |
| `examples/` | Example feature request and expected artifact map |

## Best Fit

Use this for one substantial feature that needs production-quality integration, not tiny edits.

Good examples:

- permissions and roles system
- billing integration
- dashboard redesign with backend changes
- search and filtering across multiple data models
- onboarding flow with email, auth, analytics, and UI
- migration from one provider/API to another

Bad examples:

- typo fixes
- one small component
- isolated bug fix with obvious cause
- quick config change

## License

MIT
