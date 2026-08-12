---
name: fresh-git-workflow
description: Prepares safe, owner-executed Git and GitHub handoffs only for the local Fresh repository, including read-only readiness checks, branch names, commit messages, exact staged paths, push commands, draft pull request titles/bodies, and post-action verification. Use when planning a Fresh branch, preparing a commit, publishing a completed goal, describing a PR, checking readiness, or verifying Git actions the owner performed manually.
---

# Fresh Git Workflow

Prepare Git publication instructions for Fresh without touching any other repository. A finished edit is not automatically publishable, and publication remains an owner action even after the gate is clean.

## Owner-managed Git boundary

Codex must not perform any Git or GitHub operation that changes state. Do not:

- create, switch, rename, or delete a branch;
- stage or unstage files;
- commit, amend, rebase, merge, revert, or cherry-pick;
- push, pull, fetch, or change remotes/configuration;
- create, edit, close, mark ready, or merge a pull request;
- invoke `$github:yeet` or another publishing automation.

Read-only commands such as `git status`, `git diff`, `git log`, `git show`, `git branch -vv`, `git remote -v`, and `git rev-parse` are allowed when scoped to Fresh. After a clean gate, give the owner copyable instructions instead of executing them. If the owner later reports a manual action, verify it read-only and report discrepancies; do not repair Git state automatically.

## Hard scope boundary

Before preparing any Git handoff, resolve and print:

```text
Expected worktree: /Users/ibnutaufickahraza/Swift/Fresh
Repository root: <git rev-parse --show-toplevel>
Current branch: <git branch --show-current>
Remote: <git remote -v>
```

Stop if the resolved repository root is not exactly `/Users/ibnutaufickahraza/Swift/Fresh`. Never run Git with another working directory, traverse into a neighboring repo, or change another repo's remote/config.

Never request credentials or embed tokens in commands. Never recommend force-push, rewriting published history, destructive reset/clean, or deleting local/remote branches. If such an operation is genuinely needed, stop and explain the risk; this skill does not authorize it.

## Publication quality gate

Do not describe a goal as ready for the owner's commit/push/PR until every item is true:

1. Goal ID, outcome summary, spec, and acceptance criteria exist.
2. `git status` and the complete intended diff were inspected.
3. Scope contains no unrelated files or secrets.
4. Relevant build/tests and required manual checks passed recently against the current working tree.
5. A context-clean reviewer inspected the current result using `$fresh-code-review`.
6. The latest reviewer returned `Verdict: No material findings.`
7. Any earlier finding is fixed or explicitly accepted by the user with its risk documented.

If one item is false, return `Publication blocked` with the missing evidence and the next safe non-Git action. Do not suggest a checkpoint/WIP commit.

After any repair, verification and a new fresh review are required. The reviewer that raised a finding does not approve its own fix.

## Branch model

- G00 initial agentic baseline was manually committed and pushed by the owner to `main` as `bf7e711` (`init: project agent markdown`). Preserve that published history; do not ask the owner to amend it merely to change the subject.
- Recommend that the owner create `dev` from the accepted G00 `main` baseline.
- Recommend that every later goal start from current `dev` using `feature/gXX-short-kebab-name`.
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

The owner already published G00 with a different subject. Preserve it. Recommend a new subject only for the current uncommitted goal or repair; never reuse a historical recommendation merely to make the log look uniform.

## Read-only preparation workflow

1. Run read-only orientation: `pwd`, repo root, branch, status, remotes, recent log.
2. Inspect untracked and tracked scope; search filenames and diff for likely secrets.
3. Confirm the publication quality gate.
4. Enumerate exact intended paths; never stage them.
5. Recommend one commit subject and determine the intended branch/base/push/PR metadata.
6. Produce the manual handoff below.
7. After the owner acts, verify branch/upstream/commit/status read-only when requested or when needed before starting the next goal.

Never recommend amending a published commit just to improve its message. A later documentation correction receives a new commit after its own gate.

## GitHub repository and remote

Default repository proposal for this personal project:

- Name: `Fresh`.
- Visibility: private.
- Description: `A native iOS app that helps prioritize food before it is forgotten.`
- Initialize remotely with README/license/gitignore: no, because the local repository already contains project history.

The owner manages repository creation, authentication, visibility, and remote configuration. Codex may inspect the configured remote read-only and flag a mismatch, but must not create/repurpose a repository, log in, or change `origin`.

## Manual handoff

Only after the gate passes, provide one self-contained block in this order:

1. `Status`: `Ready for manual Git` or `Publication blocked`.
2. Goal outcome and final reviewer verdict.
3. Intended branch and base.
4. Exact relative paths to stage. Prefer explicit paths; suggest `git add -A` only when the complete worktree is proven in scope and list that fact.
5. Recommended commit subject.
6. Copyable commands for the owner. Include `cd /Users/ibnutaufickahraza/Swift/Fresh`, orientation, branch creation/switch when required, staging, `git diff --cached --check`, `git diff --cached --stat`, commit, push, and final status/log checks.
7. For feature goals, draft PR base/title/body. For milestone promotion, target `main` only after explicit owner approval.
8. A short expected-result checklist so the owner can report success or paste an error.

Commands are instructions for the owner, not authorization for Codex to execute them.

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

Ask the owner to open feature PRs as draft by default. The owner alone marks ready or merges.

## Handoff format

After an owner-reported publication action, verify read-only where local evidence permits and report:

- goal and outcome summary;
- branch and base;
- commit hash and subject;
- remote repository;
- PR URL and draft/ready state, if created;
- verification evidence and final fresh-review verdict;
- any remaining owner action or evidence that could not be verified locally.
