# Fresh Agent Guide

## Project

Fresh is a personal native iOS SwiftUI app that helps people prioritize food before it is forgotten. It offers transparent freshness estimates; it must never claim that food is definitely safe or unsafe.

Read these before planning a feature:

- `docs/superpowers/specs/2026-08-12-fresh-agentic-development-design.md`
- `docs/Development/PRODUCT_ROADMAP.md`
- `docs/Development/WORKFLOW.md`
- Relevant files under `Fresh/Docs/ScreenSpecs/`
- `docs/decisions/DECISION_LOG.md`

## Architecture

- Use lightweight feature-first SwiftUI structure.
- Features may depend on Core and DesignSystem; Core must not depend on Features.
- Keep freshness rules deterministic and outside Views.
- SwiftData is the persistence layer. Surface meaningful save failures.
- On-device intelligence is optional interpretation only; the app and rule engine must work without it.
- Add protocols only at real substitution/test boundaries.

## Development loop

1. Identify one roadmap goal and state its outcome summary.
2. Write/update its spec and acceptance criteria.
3. Use `$superpowers:writing-plans` before multi-step implementation.
4. Use `$superpowers:test-driven-development` for behavior and bug fixes.
5. Implement the smallest coherent slice and verify it.
6. Use a new context-clean read-only sub-agent with `$fresh-code-review`.
7. Validate findings, repair valid issues, rerun verification, then spawn a different fresh reviewer.
8. Finish only after the latest reviewer says `Verdict: No material findings.`

If the same root problem survives three repair/re-review cycles, stop patching, perform root-cause analysis, and ask the user before expanding architecture or scope.

## Swift guidance

Use project-local skills when relevant:

- `$swiftui-pro` for native SwiftUI, navigation, state, design, performance, and accessibility.
- `$swiftdata-pro` for models, persistence, queries, predicates, and relationships.
- `$swift-concurrency-pro` for async/await, tasks, actors, isolation, cancellation, and Sendable.
- `$swift-testing-pro` for Swift Testing unit/integration tests; UI tests stay XCTest.

Installed Xcode/toolchain and project build settings are authoritative. Do not upgrade Swift, iOS target, packages, or add third-party dependencies without explicit user approval.

## Verification

Discover the available scheme/destination before hard-coding simulator names. Typical commands:

```bash
xcodebuild -project Fresh.xcodeproj -scheme Fresh -showdestinations
xcodebuild -project Fresh.xcodeproj -scheme Fresh -destination 'platform=iOS Simulator,name=<available device>' build
xcodebuild -project Fresh.xcodeproj -scheme Fresh -destination 'platform=iOS Simulator,name=<available device>' test
```

Prefer focused tests during iteration, then full applicable build/test before review. Also inspect relevant empty, error, unavailable, Dynamic Type, VoiceOver, Light/Dark, Increase Contrast, and Reduce Motion states.

Never claim a command passed unless its current output was observed.

## Git and GitHub

Use `$fresh-git-workflow`. Git publication is owner-managed: Codex may inspect Git state read-only, but must not create/switch branches, stage, commit, push, open/update a PR, merge, or change Git/GitHub configuration. After the whole goal passes acceptance criteria, verification, diff/secret inspection, and a fresh reviewer returns no material findings, give the owner a complete manual Git handoff. Work only in `/Users/ibnutaufickahraza/Swift/Fresh`.

- Initial G00 baseline: `main` after quality gate.
- Integration: `dev`.
- Later goals: `feature/gXX-short-name`, based on `dev`, PR back to `dev`.
- Milestone promotion: `dev` to `main` only when the user approves.

The handoff must state the goal, intended branch/base, exact paths to stage, commit subject, commands, PR title/body when relevant, and checks the owner should observe. Never recommend force-push, published-history rewrites, branch deletion, or operations in another repository.

## Scope and quality

- Preserve user changes and keep unrelated changes out of the goal.
- No hidden fake defaults: unknown input remains unknown.
- No placeholder TODO in behavior claimed complete.
- Do not add recipe, shopping list, nutrition, household sharing, barcode/OCR, cloud sync, or analytics features unless a later approved goal adds them.
- UI must be native, calm, accessible, and consistent with `Fresh/Docs/DESIGN_SYSTEM.md`.
- `Fresh/Docs` lives inside an Xcode file-synchronized group. Whenever a new documentation file is added there, add it to the Fresh target's `PBXFileSystemSynchronizedBuildFileExceptionSet` and verify the built `.app` contains no unintended Markdown.
- Every completed goal report includes outcome, changes, verification, fresh-review cycles, known risk, branch, and commit status.

## Decision memory

Record a concise Markdown decision before or alongside work that depends on it. Update `docs/decisions/DECISION_LOG.md` when a conversation changes product scope, architecture, data/safety/privacy behavior, navigation/critical copy, platform/dependencies, agent workflow, quality gates, Git/release policy, or selects one meaningful option over another.

Do not paste raw chat transcripts. Capture date, context, considered options, decision, rationale, consequences, status, and revisit trigger. Minor implementation details that are easy to reverse do not need an entry. If a later decision replaces an older one, preserve history and mark the old entry superseded.
