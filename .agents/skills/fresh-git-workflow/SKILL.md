---
name: fresh-git-workflow
description: Safely manages Git and GitHub work only for the local Fresh repository, including goal branches, quality-gated commits, remotes, pushes, draft pull requests, titles, descriptions, and handoff summaries. Use when creating or naming a Fresh branch, preparing a commit, publishing a completed goal, opening or updating a PR, or checking whether code is ready for GitHub.
---

# Fresh Git Workflow

Manage Git publication for Fresh without touching any other repository. A finished edit is not automatically publishable.

## Hard scope boundary

Before any Git write, resolve and print:

```text
Expected worktree: /Users/ibnutaufickahraza/Swift/Fresh
Repository root: <git rev-parse --show-toplevel>
Current branch: <git branch --show-current>
Remote: <git remote -v>
```

Stop if the resolved repository root is not exactly `/Users/ibnutaufickahraza/Swift/Fresh`. Never run Git with another working directory, traverse into a neighboring repo, or change another repo's remote/config.

Never expose credentials, embed tokens in a remote URL, force-push, rewrite published history, delete remote branches, or use destructive reset/clean commands unless the user explicitly requests the exact action and its target is verified.

## Publication quality gate

For work performed by an agent, do not commit, push, or open a PR until every item is true:

1. Goal ID, outcome summary, spec, and acceptance criteria exist.
2. `git status` and the complete intended diff were inspected.
3. Scope contains no unrelated files or secrets.
4. Relevant build/tests and required manual checks passed recently against the current working tree.
5. A context-clean reviewer inspected the current result using `$fresh-code-review`.
6. The latest reviewer returned `Verdict: No material findings.`
7. Any earlier finding is fixed or explicitly accepted by the user with its risk documented.

If one item is false, return `Publication blocked` with the missing evidence and the next safe action. Do not create a checkpoint commit unless the user explicitly overrides this project policy.

After any repair, verification and a new fresh review are required. The reviewer that raised a finding does not approve its own fix.

## Branch model

- G00 initial agentic baseline may commit directly to `main` after its gate is clean.
- Create `dev` from the accepted G00 `main` baseline.
- Every later goal starts from current `dev` using `feature/gXX-short-kebab-name`.
- Merge goal PRs into `dev`.
- Promote `dev` to `main` only for a user-approved milestone.
- One feature branch contains one roadmap goal; split materially independent scope instead of hiding it in one PR.

Examples:

```text
feature/g01-app-shell
feature/g02-freshness-domain
feature/g05-add-and-estimate
```

Do not use the generic GitHub plugin's `agent/...` default branch prefix in this repo; this project policy is more specific.

## Commit convention

Use one coherent post-gate commit per small goal by default. Larger goals may use several verified commits only when each represents a meaningful behavior.

Format:

```text
<type>(<optional scope>): <imperative summary>
```

Allowed types:

- `feat`: user-facing behavior.
- `fix`: defect correction.
- `test`: test-only change.
- `docs`: documentation-only change.
- `refactor`: behavior-preserving code structure.
- `chore`: tooling, configuration, or project foundation.

Rules: lower-case type, no trailing period, aim for 72 characters or fewer, state the outcome rather than file activity. Never add co-author attribution unless the named person explicitly contributed and wants it.

G00 planned commit:

```text
chore: establish Fresh agentic project foundation
```

## Safe local workflow

1. Run read-only orientation: `pwd`, repo root, branch, status, remotes, recent log.
2. Inspect untracked and tracked scope; search filenames and diff for likely secrets.
3. Confirm the publication quality gate.
4. Stage explicit intended paths. Use `git add -A` only when the entire worktree is confirmed in scope.
5. Inspect `git diff --cached --stat` and `git diff --cached`.
6. Commit with the approved message.
7. Verify the new commit summary and ensure the worktree is clean or only contains known unrelated changes.

Do not amend a published commit. Do not automatically amend a local commit after hooks; create a new commit unless the user asks to amend.

## GitHub repository and remote

Default repository proposal for this personal project:

- Name: `Fresh`.
- Visibility: private.
- Description: `A native iOS app that helps prioritize food before it is forgotten.`
- Initialize remotely with README/license/gitignore: no, because the local repository already contains project history.

Before creating the remote, verify the authenticated GitHub owner and that `owner/Fresh` does not already exist. Never overwrite or repurpose an existing remote repository. Add `origin` only after matching owner, repository name, and URL.

The GitHub publish workflow requires authenticated `gh`. If `gh` is missing or unauthenticated, stop and provide the exact prerequisite; do not use a browser session, raw token, or unofficial API workaround.

## Push and PR workflow

Use the installed GitHub `yeet` skill after this project gate passes, while preserving Fresh-specific branch names and base rules.

1. Push current branch with tracking to the verified `origin`.
2. For feature goals, open a draft PR from `feature/gXX-...` to `dev`.
3. For milestone promotion, open a separate PR from `dev` to `main` only when requested.
4. Never claim push/PR success without checking the returned remote/URL.

PR title format:

```text
[GXX] Outcome-oriented goal title
```

PR body:

```markdown
## Ringkasan hasil
What the user can now do.

## Perubahan
- Major behavior or structure changes.

## Verifikasi
- `command` — PASS
- Manual/simulator check — PASS

## Fresh review
- Review cycles: N
- Final verdict: No material findings

## Risiko dan batas scope
- Known risks, deferred items, and explicit exclusions.

## Checklist
- [x] Acceptance criteria met
- [x] Relevant build/tests pass
- [x] Current diff reviewed
- [x] Fresh reviewer clean
```

Open as draft by default. Mark ready or merge only when the user explicitly requests that next external action and required checks remain green.

## Handoff format

After a successful publication action, report:

- goal and outcome summary;
- branch and base;
- commit hash and subject;
- remote repository;
- PR URL and draft/ready state, if created;
- verification evidence and final fresh-review verdict;
- any remaining user action.
