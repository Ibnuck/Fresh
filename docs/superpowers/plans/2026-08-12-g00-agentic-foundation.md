# G00 Fresh Agentic Foundation Implementation Plan

> Goal type: repository foundation and documentation; no application feature behavior is implemented in G00.

## Outcome summary

After G00, a new coding chat can independently understand Fresh, follow a lightweight spec/plan/test/review loop, delegate final review to a context-clean read-only sub-agent, prepare image-generation handoffs from detailed native iOS screen specs, and publish only quality-gated work to the correct GitHub repository.

## Scope

### In scope

- Research and approved agentic design.
- Root `AGENTS.md`, repo-local Codex config, and read-only reviewer role.
- Four audited Swift reference skills.
- Custom Fresh code-review and Git workflow skills.
- Goal roadmap with observable outcome summaries and branch names.
- Durable decision memory, project journal, and reusable new-project playbook.
- Detailed `.gitignore` for Xcode/Swift and local tools.
- Lightweight SwiftUI architecture documentation.
- Standalone visual handoff, design system, template, and eight MVP screen specs.
- Validation evidence and final fresh review of the complete G00 tree.
- Planned first commit metadata; no commit/push before the gate passes.

### Out of scope

- Changing the Hello World application behavior.
- Creating production SwiftData models, navigation, or app screens.
- Generating mockup images in this conversation.
- Installing MCP servers or a custom plugin.
- Publishing until authenticated GitHub remote verification and the complete quality gate pass.

## Acceptance criteria

- [x] A fresh chat can find concise durable guidance in `AGENTS.md`.
- [x] Every G00–G10 roadmap goal has a branch and plain-language outcome summary.
- [x] Material decisions have context, alternatives, rationale, consequences, and revisit triggers in Markdown.
- [x] The reusable playbook is understandable by a new project chat without this conversation.
- [x] Reviewer configuration is read-only and calls the project review skill.
- [x] Review skill produces consistent evidence-based P0–P3 findings and a verdict under pressure tests.
- [x] Git skill blocks commit/push/PR when verification or a clean fresh verdict is absent.
- [x] SwiftUI, SwiftData, concurrency, and Swift Testing skills are project-local and audited.
- [x] Visual handoff is understandable without this conversation and covers every MVP screen.
- [x] `.gitignore` ignores generated, personal, secret, and tool artifacts while tracking source/config/docs/skills and `Package.resolved`.
- [x] Current Xcode project build/tests applicable to the untouched starter app pass.
- [x] Markdown, TOML, YAML/frontmatter, links, and skill structure pass available validation.
- [x] A context-clean reviewer evaluates the complete G00 tree and returns `Verdict: No material findings.`; a second final-tree record check is required before handoff.
- [ ] Git remote owner/repository/visibility/history are authenticated and verified before first push.

## Task checklist

### Task 1 — Discover and research

Ringkasan hasil: agentic choices are grounded in the existing Fresh research and current official guidance.

- [x] Read repository Markdown and Xcode project state.
- [x] Research Codex AGENTS.md, skills, sub-agents, plugins, and execution plans.
- [x] Choose the Lightweight Agentic Loop and defer unnecessary integrations.

### Task 2 — Design product, architecture, and review loop

Ringkasan hasil: the project has an approved, bounded design before application coding.

- [x] Document feature-first SwiftUI boundaries and MVP screens.
- [x] Document fresh reviewer packet, finding format, repair loop, and stopping condition.
- [x] Add goal outcomes and Git branch model.

### Task 3 — Install audited Swift skills

Ringkasan hasil: implementation/review chats have current focused guidance for native Swift development.

- [x] Audit and install `swiftui-pro`.
- [x] Audit and install `swiftdata-pro`.
- [x] Audit and install `swift-concurrency-pro`.
- [x] Audit and install `swift-testing-pro`.
- [x] Complete structural validation in the current environment.

### Task 4 — Create and pressure-test project skills

Ringkasan hasil: repeated Fresh workflows become explicit, testable project-local skills.

- [x] Capture five no-skill code-review baselines.
- [x] Create `fresh-code-review` and run five fresh forward tests.
- [x] Capture no-skill Git publication baselines.
- [x] Create `fresh-git-workflow` and run five fresh forward tests.
- [x] Evaluate a separate feature-cycle skill; omit it because three fresh baselines already followed the complete cycle from `AGENTS.md` and repo docs, so another skill would duplicate context.
- [x] Record validation evidence and refinements.

### Task 5 — Create durable repo guidance

Ringkasan hasil: new chats know the architecture, roadmap, commands, review gate, and publication policy.

- [x] Add `AGENTS.md`, README, architecture, workflow, roadmap, and review-record guidance.
- [x] Add decision log/template, project journal, and reusable project playbook.
- [x] Add `.codex/config.toml` and `.codex/agents/reviewer.toml`.
- [x] Add detailed `.gitignore`.
- [x] Validate configuration syntax and references.

### Task 6 — Create standalone visual handoff

Ringkasan hasil: an external image-generation chat can create consistent mockups and return reviewable Markdown without conversation context.

- [x] Add start-here handoff, design system, generation guide, and templates.
- [x] Add detailed specs for Onboarding, Today, My Food, Quick Add, Estimate Review, Food Detail, Edit Food, and Settings.
- [x] Run automated consistency/accessibility/scope structure checks across all screen specs.

### Task 7 — Verify complete G00 tree

Ringkasan hasil: the foundation is internally consistent and does not break the existing starter app.

- [x] Validate skills, TOML, Markdown references, frontmatter, and ignored/tracked file intent.
- [x] Discover available Xcode simulator destination.
- [x] Run applicable build and test commands.
- [x] Inspect full intended scope and scan for secrets/unrelated content.

### Task 8 — Fresh final review and repair loop

Ringkasan hasil: an independent context-clean reviewer confirms G00 meets its complete contract.

- [x] Spawn reviewer A with the complete G00 packet.
- [ ] Verify and repair valid findings; rerun checks.
- [ ] Spawn a new reviewer after every repair.
- [x] Save the clean review record; run the post-record final-tree check.

### Task 9 — Publication gate

Ringkasan hasil: the first stable baseline is ready for GitHub without risking another repo or publishing unreviewed work.

- [x] Owner manually committed and pushed the initial baseline through Xcode as `bf7e711` (`init: project agent markdown`).
- [x] Verify local `main`, `origin/main`, configured `origin`, tracked-file count, and clean working tree after the owner's push.
- [x] Record DEC-010: all future Git/GitHub writes are owner-managed; Codex provides instructions only.
- [ ] Owner confirms the GitHub repository's intended private visibility; local Git cannot prove visibility without authenticated GitHub metadata.
- [ ] Create `dev` after the accepted `main` baseline; do not start G01 yet.

## Verification record

Fill this section with exact commands and observed results. `Reported passing` is not equivalent to `reviewer verified`.

| Check | Command/evidence | Result |
|---|---|---|
| Skill structure | official `quick_validate.py` on all six skills | PASS |
| TOML/YAML/frontmatter | Python `tomllib`, Ruby Psych, and official skill validator | PASS |
| Markdown links/content | local-link scan + eight screen-spec structural checks | PASS |
| Xcode build | clean build, iPhone 17 Pro simulator, iOS 26.5 | PASS |
| Unit/UI tests | final `xcodebuild test`; 7 executions, 0 failures | PASS |
| App bundle hygiene | inspect `Fresh.app` after clean build | PASS; 0 Markdown files bundled |
| Full scope/secret inspection | all untracked/intended paths listed; secret/large/executable/ignored-file checks | PASS |
| Final fresh review | context-clean full-tree cycle 1 | PASS; post-record check pending |
| Owner publication | `bf7e711`; local `main` and `origin/main` aligned; 105 tracked, 0 untracked | PASS locally; remote visibility remains owner-confirmed |

## Planned publication metadata

- Initial branch: `main`.
- Actual owner-created commit: `bf7e711` — `init: project agent markdown`.
- Do not amend published history merely to replace the subject with the earlier recommendation.
- G00 PR: none; first verified baseline goes directly to the empty `main`.
- Later integration branch: `dev`.
- First feature branch: `feature/g01-app-shell`.
- First feature PR base/title: `dev`, `[G01] Establish the Fresh app shell`.
