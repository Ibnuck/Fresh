# Fresh Development Workflow

## Simple operating model

Fresh uses one main implementation agent and one fresh read-only reviewer at a time. Specs, tests, the built app, and observed tool output are the source of truth. Plugins and extra agents are added only for a proven recurring need.

## Goal cycle

```text
Goal outcome
  → spec and acceptance criteria
  → implementation plan
  → failing test where applicable
  → minimal implementation
  → focused then full verification
  → fresh read-only reviewer
  → validated repairs
  → new fresh reviewer
  → clean quality gate
  → manual Git handoff
  → owner commits / pushes / opens draft PR
```

## Goal packet

Before coding, record:

- goal ID and branch;
- outcome summary: what the user can do afterward;
- in-scope and out-of-scope behavior;
- acceptance criteria;
- file/task plan;
- relevant screen specs;
- required unit, integration, UI, accessibility, and manual checks.

## Decision capture

Before implementation, inspect `docs/decisions/DECISION_LOG.md`. If brainstorming or review produces a material choice, append a concise record using `docs/decisions/DECISION_TEMPLATE.md`. Do not erase earlier reasoning; mark it superseded when a newer decision replaces it. Routine code details stay in the plan or code, not the decision log.

## Review packet

Use `.agents/skills/fresh-code-review/references/review-packet-template.md`. Every repair receives a new reviewer without the previous conversation or review opinion. The main agent verifies feedback; it does not apply comments blindly.

## Stopping rules

- Clean: latest fresh reviewer has no material findings and verification is green.
- Repair: a finding is reproduced/validated, fixed, regression-covered where appropriate, and reverified.
- Root-cause pause: the same problem remains after three cycles.
- User decision: the fix needs new feature scope, architecture, dependency, privacy policy, or external authority.

## Publication

Use `$fresh-git-workflow`. Git is owner-managed: the agent performs read-only inspection and never creates/switches branches, stages, commits, pushes, opens/updates PRs, merges, or changes Git/GitHub configuration. After the full goal gate is clean, the agent provides a manual handoff containing:

- intended branch and base;
- exact files to stage;
- one recommended commit subject;
- copyable commands for status, staging, cached-diff inspection, commit, and push;
- draft PR base, title, and body when relevant;
- expected verification after each external action.

G00 was manually published by the owner to `main` as commit `bf7e711` (`init: project agent markdown`). Later goals use `feature/gXX-name` into `dev`. The agent may verify a completed owner action read-only, but must not continue with another Git write.

## Completion summary

```markdown
## GXX — Goal name

Ringkasan hasil: <observable user capability>

- Yang berubah: ...
- Verifikasi: ...
- Review fresh: <N cycles>; final verdict ...
- Risiko tersisa: ...
- Branch/commit/PR: ...
```
