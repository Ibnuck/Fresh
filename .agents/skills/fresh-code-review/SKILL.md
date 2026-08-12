---
name: fresh-code-review
description: Performs a context-clean, evidence-based, read-only quality gate for the Fresh iOS app. Use after implementing or repairing a goal or mini-feature, before merge or completion, and whenever a fresh sub-agent must review Swift, SwiftUI, SwiftData, concurrency, tests, accessibility, food-safety wording, privacy, or regression risk without editing code.
---

# Fresh Code Review

Review one Fresh goal independently. Find material defects; do not manufacture criticism and do not modify the repository.

## Non-negotiable role

- Stay read-only. Do not patch, format, commit, stage, or push.
- Treat the goal spec and acceptance criteria as the contract.
- Treat code, build output, and test output as evidence; a green summary is not proof of adequate coverage.
- Report correctness, regression, data loss, safety wording, privacy, accessibility, performance with user impact, and meaningful test gaps.
- Omit style preferences and speculative architecture advice unless they cause a concrete failure.
- Never call an item `safe to eat`, `unsafe to eat`, or otherwise infer food safety from a freshness estimate.
- Return `No material findings` when the evidence supports it.

## Required review packet

Ask for a missing item only when it prevents a defensible review. Otherwise state the limitation and continue.

1. Goal ID and one-paragraph outcome summary.
2. Spec and acceptance criteria.
3. Changed-file list or diff.
4. Latest build and test results.
5. Explicit out-of-scope areas.

Read the changed files plus the smallest relevant execution path. Do not expand into an unrelated whole-repository audit.

## Review workflow

1. Read the spec before the implementation.
2. Translate each acceptance criterion into an observable behavior.
3. Inspect changed code and callers/callees that can invalidate that behavior.
4. Cross-check relevant technical guidance:
   - Use `$swiftui-pro` for SwiftUI API, navigation, state, performance, native design, and accessibility.
   - Use `$swiftdata-pro` for models, queries, persistence, relationships, predicates, and save semantics.
   - Use `$swift-concurrency-pro` only when async work, tasks, actors, isolation, cancellation, or sendability is present.
   - Use `$swift-testing-pro` for unit/integration tests; remember UI tests remain XCTest.
5. Verify boundary, empty, error, unavailable, and retry paths that are relevant to the goal.
6. Compare claimed verification with the tests that actually ran. Never claim to have run a command you did not run.
7. Deduplicate findings by root cause. Keep distinct defects separate even when they occur on the same line.
8. Rank only after establishing evidence.

The installed toolchain and project build settings override version assumptions inside reference skills. Do not demand an unrequested Swift or deployment-target upgrade.

## Priority rules

- `P0`: release-blocking catastrophic impact such as broad irreversible data loss or a critical security/privacy breach.
- `P1`: material incorrect behavior, crash, silent data loss, prohibited safety claim, or primary acceptance criterion failure.
- `P2`: meaningful secondary behavior, accessibility, recovery, performance, or coverage problem with concrete impact.
- `P3`: low-risk maintainability issue only when it is likely to cause a near-term defect. Do not use P3 for taste.

## Finding format

Write one defect per finding, ordered P0 to P3:

```markdown
- [P1] Short actionable title — `path/File.swift:42`
  - Impact: What user or system behavior fails.
  - Evidence: Exact execution path, condition, or reproducible scenario.
  - Contract: Acceptance criterion or project rule that is violated.
  - Test gap: Missing regression test, or `Covered by <test>` when applicable.
```

Do not include a code patch. The implementation agent owns diagnosis and repair. If verification cannot be independently rerun, distinguish `reported passing` from `reviewer verified`.

## Completion

End with exactly one of:

- `Verdict: Changes required.`
- `Verdict: No material findings.`

Then add a one-line verification note listing what was personally inspected or run.
