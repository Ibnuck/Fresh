# Fresh Decision Log

This is the durable source for material decisions from project conversations. Entries summarize reasoning and consequences; they are not raw transcripts.

## Index

| ID | Date | Status | Decision |
|---|---|---|---|
| DEC-001 | 2026-08-12 | accepted | Use a lightweight agentic workflow. |
| DEC-002 | 2026-08-12 | accepted | Require context-clean reviewer loops and a hard publication gate. |
| DEC-003 | 2026-08-12 | accepted | Use lightweight feature-first native SwiftUI architecture. |
| DEC-004 | 2026-08-12 | accepted | Make Markdown the visual source of truth; no visual companion website. |
| DEC-005 | 2026-08-12 | accepted | Keep freshness deterministic and AI optional/non-authoritative. |
| DEC-006 | 2026-08-12 | accepted | Use a focused project-local skill portfolio. |
| DEC-007 | 2026-08-12 | accepted | Use main/dev/one-feature-branch-per-goal Git flow. |
| DEC-008 | 2026-08-12 | accepted | Record outcome summaries and material decisions as project memory. |
| DEC-009 | 2026-08-12 | accepted | Use free-text food context and generated category; keep ripeness inside condition. |
| DEC-010 | 2026-08-13 | accepted | Make all Fresh Git/GitHub writes owner-managed. |

---

## DEC-001 — Lightweight agentic workflow

- Date: 2026-08-12
- Status: accepted
- Scope: workflow
- Related goal: G00
- References: `docs/superpowers/specs/2026-08-12-fresh-agentic-development-design.md`

### Context

The project needed specs, plans, agents, skills, reviews, and optional plugins, but it is a personal app and should remain understandable by one developer.

### Options considered

1. Minimal `AGENTS.md` only: simple, but too weak for the requested independent quality loop.
2. Lightweight agentic loop: main agent, durable docs, focused skills, fresh reviewer, and tests.
3. Full orchestrator with many roles, hooks, MCP servers, Spec Kit, and plugins: powerful but disproportionate.

### Decision

Use the lightweight loop. Add complexity only after a recurring problem demonstrates that a new tool improves outcomes.

### Consequences and revisit trigger

The workflow stays readable and token-conscious. Plugins/MCP/extra roles are deferred until a concrete repeated external-integration need appears.

---

## DEC-002 — Context-clean review and publication gate

- Date: 2026-08-12
- Status: accepted
- Scope: quality, workflow, Git
- Related goal: project-wide
- References: `.agents/skills/fresh-code-review/SKILL.md`, `.agents/skills/fresh-git-workflow/SKILL.md`

### Context

The owner wants each completed coding goal evaluated by a new sub-agent with no exposure to the implementation conversation, followed by repair and a new reviewer until clean.

### Decision

After implementation and verification, spawn a context-clean read-only reviewer with the minimal goal packet. Validate findings, repair material issues, rerun verification, and spawn a different fresh reviewer. No agent-created commit, push, or PR is allowed until the latest reviewer returns `Verdict: No material findings.`

### Consequences and revisit trigger

Reviews cost more tokens but reduce confirmation bias. After the same root cause survives three cycles, stop patching and perform root-cause analysis before changing architecture/scope.

Publication still requires this clean gate. The earlier implication that an agent might execute Git writes after the gate is superseded by DEC-010; the owner now performs every Git/GitHub mutation.

---

## DEC-003 — Feature-first native SwiftUI architecture

- Date: 2026-08-12
- Status: accepted
- Scope: architecture
- Related goal: G01 onward
- References: `docs/Development/ARCHITECTURE.md`

### Context

Fresh needs testable SwiftUI/SwiftData code without the ceremony of a large Clean Architecture project.

### Decision

Use Views → `@Observable` feature models → narrow services/repositories → SwiftData and deterministic rules. Organize by feature, keep business rules out of Views, and create protocols only at real substitution boundaries.

### Consequences and revisit trigger

The architecture remains approachable. Add layers only when a real feature cannot remain testable or maintainable within these boundaries.

---

## DEC-004 — Markdown-first visual handoff

- Date: 2026-08-12
- Status: accepted
- Scope: UX, workflow
- Related goal: G00 and all UI goals
- References: `Fresh/Docs/VISUAL_HANDOFF_README.md`

### Context

A temporary web visual companion was confusing and wasteful for this project. The owner will use another GPT image-generation chat, then return its Markdown proposal.

### Decision

Do not build or use a visual companion web app. Keep the design system, generation guide, exact screen layout/state specs, and generated proposals in Markdown. External images remain proposals until reviewed and incorporated into the source specs.

### Consequences and revisit trigger

Any chat can read the handoff without local web state. Reconsider tooling only if manual Markdown handoff repeatedly causes inconsistency that structured files cannot resolve.

---

## DEC-005 — Deterministic freshness; optional AI

- Date: 2026-08-12
- Status: accepted
- Scope: product, safety, AI
- Related goal: G02 and G09
- References: `Fresh/Docs/APP_CONCEPT_RESEARCH.md`, `docs/Development/ARCHITECTURE.md`

### Context

AI can help interpret ambiguous user input, but freshness guidance must remain explainable and must not become an unsupported food-safety verdict.

### Decision

Use bundled deterministic freshness rules as the source of estimates. On-device AI may interpret input but is optional, never supplies safety facts, never blocks core features, and must have unavailable/invalid-output fallbacks.

### Consequences and revisit trigger

The app remains usable without AI and can show assumptions/source/confidence. Revisit only when a new intelligence feature preserves these safety and fallback boundaries.

---

## DEC-006 — Focused project-local skill portfolio

- Date: 2026-08-12
- Status: accepted
- Scope: workflow
- Related goal: G00
- References: `docs/Development/Reviews/G00-SKILL-VALIDATION.md`

### Context

The Swift skill catalog contains many skills. Installing everything would add noise and third-party instruction risk.

### Decision

Audit and install only `swiftui-pro`, `swiftdata-pro`, `swift-concurrency-pro`, and `swift-testing-pro`. Add custom `fresh-code-review` and `fresh-git-workflow` because pressure tests demonstrated gaps. Do not add `fresh-feature-cycle`: fresh agents already followed that workflow from repo guidance, so it would duplicate context.

### Consequences and revisit trigger

Skill discovery stays focused. Add another skill only after a failing baseline proves a recurring behavior gap.

---

## DEC-007 — Git branches and first baseline

- Date: 2026-08-12
- Status: accepted
- Scope: Git, release
- Related goal: project-wide
- References: `.agents/skills/fresh-git-workflow/SKILL.md`, `docs/Development/PRODUCT_ROADMAP.md`

### Context

The repository begins without history. The owner wants the foundation on main, then dev and one feature branch per goal.

### Decision

After G00's complete quality gate, create the first coherent commit directly on `main`. Then create `dev`. Each later goal uses `feature/gXX-short-name` from `dev` and a draft PR back to `dev`; milestone promotion to `main` requires user approval.

### Consequences and revisit trigger

No empty/WIP commits or pushes are created by agents. Revisit only if collaboration scale or release cadence makes a different model materially simpler.

---

## DEC-008 — Outcome and decision memory

- Date: 2026-08-12
- Status: accepted
- Scope: workflow, documentation
- Related goal: project-wide
- References: `docs/decisions/README.md`, `docs/REUSABLE_PROJECT_PLAYBOOK.md`

### Context

Future chats need to understand not only what was built, but why important choices were made. The owner also wants the Fresh process reusable for new projects.

### Decision

Every roadmap goal has a plain-language outcome summary. Material conversations are summarized in this decision log with alternatives, rationale, consequences, and revisit triggers. A separate reusable playbook describes how to bootstrap another project using the proven process.

### Consequences and revisit trigger

Documentation requires small ongoing updates but reduces repeated explanation and accidental reversals. Split entries into individual ADR files only if this single log becomes difficult to scan.

---

## DEC-009 — Free-text context and generated category

- Date: 2026-08-12
- Status: accepted
- Scope: product, UX, data, AI
- Related goal: G05 and G09
- References: `Fresh/Docs/APP_CONCEPT_RESEARCH.md`, `Fresh/Docs/ScreenSpecs/04_QUICK_ADD.md`, `Fresh/Docs/ScreenSpecs/05_ESTIMATE_REVIEW.md`, `Fresh/Docs/ScreenSpecs/07_EDIT_FOOD.md`

### Context

The initial Quick Add proposal used fixed choices for storage, condition, package status, and a possible separate ripeness question. The owner wants a lighter flow where people describe their food naturally and category is produced by Fresh rather than entered manually.

### Options considered

1. Fixed pickers for every attribute: easy to normalize but rigid and form-heavy.
2. Free text for storage, condition, and package; preserve raw text and normalize it internally: natural while still supporting deterministic rules.
3. Ask for fewer fields and let the Foundation Model infer missing details such as ripeness from purchase place: fastest, but creates unsupported assumptions.

### Decision

Quick Add and Edit Food use separate free-text fields for `Lokasi penyimpanan`, `Kondisi bahan`, and `Status kemasan`. Category is not a normal user-input field; Fresh derives it through the local catalog matcher and optional Foundation Model, then shows the interpretation during Estimate Review so an obvious mismatch can be corrected.

Ripeness is not a separate field. A user may include it naturally in `Kondisi bahan`, such as `alpukat masih keras`. Fresh may normalize only what the user stated. If ripeness or another detail is absent, it remains `unknown`; it is never guessed from a store, purchase place, or typical product condition.

The exact user-entered strings are retained alongside normalized internal values. Deterministic rules remain the only source of the freshness estimate. If normalization is unavailable or uncertain, local matching is attempted and unresolved values remain unknown or produce `Needs Review` rather than a false default.

### Consequences and revisit trigger

The form is simpler and accommodates everyday Indonesian phrasing, but G05/G09 must test text preservation, normalization, ambiguity, correction, and AI-unavailable fallback. Revisit only if usability testing shows free text is slower or more confusing than a small optional suggestion layer; any future suggestions must remain optional and must not replace the raw text.

---

## DEC-010 — Owner-managed Git and GitHub writes

- Date: 2026-08-13
- Status: accepted
- Scope: workflow, Git, release authority
- Related goal: project-wide
- References: `AGENTS.md`, `docs/Development/WORKFLOW.md`, `.agents/skills/fresh-git-workflow/SKILL.md`

### Context

The initial workflow allowed Codex to create branches, commit, push, and open draft pull requests after the quality gate. During G00, GitHub CLI setup was unreliable and the owner successfully committed and pushed through Xcode. The owner prefers to retain direct control of every Git/GitHub mutation and wants Codex to provide the correct commands and metadata instead.

### Options considered

1. Let Codex publish automatically after a clean gate: convenient, but conflicts with the owner's preferred control boundary.
2. Allow either party to publish depending on tool availability: flexible, but ambiguous for future chats.
3. Make publication owner-managed and Codex read-only for Git: explicit, predictable, and easy to audit.

### Decision

Use option 3. Codex may run read-only Git inspection only. Codex must not create or switch branches, stage/unstage, commit, amend, merge, rebase, push/pull/fetch, change remotes/configuration, authenticate to GitHub, create/update/merge PRs, or invoke publishing automation.

After a goal passes its complete quality gate, Codex supplies a manual Git handoff containing the intended branch/base, exact paths to stage, one commit subject, copyable commands, push target, draft PR title/body when applicable, and expected verification. The owner performs those actions. Codex may subsequently verify the local result read-only.

The existing G00 baseline was manually committed and pushed by the owner as `bf7e711` with subject `init: project agent markdown`. Published history is preserved; no amend is requested merely to improve that message.

### Consequences and revisit trigger

The owner performs a few additional commands, while accidental cross-repository or premature publication risk is reduced. Future chats must end completed goals with instructions rather than Git mutations. Revisit only if the owner explicitly replaces this policy in a later recorded decision.
