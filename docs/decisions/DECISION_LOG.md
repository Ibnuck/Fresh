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
| DEC-011 | 2026-08-13 | superseded | Regenerate the selected icon as one transparent foreground. |
| DEC-012 | 2026-08-13 | accepted | Adopt the owner-finished Liquid Glass app icon and appearance settings. |
| DEC-013 | 2026-08-13 | accepted | Generate UI screens sequentially with an asset-first visual handoff. |
| DEC-014 | 2026-08-13 | accepted | Apply proportional human-visible quality gates to generated UI assets. |
| DEC-015 | 2026-08-13 | accepted | Keep one canonical visual mockup per screen and specify remaining states in Markdown. |
| DEC-016 | 2026-08-13 | accepted | Consolidate Quick Add into one scrollable form before Estimate Review. |

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

---

## DEC-011 — Regenerate the selected icon as one transparent foreground

- Date: 2026-08-13
- Status: superseded by DEC-012
- Scope: visual identity, app icon, workflow
- Related goal: G00 visual-foundation follow-up
- References: `Design/AppIcon/APP_ICON_SPEC.md`, `Design/AppIcon/APP_ICON_COMPOSER_SPEC.md`

### Context

The owner discovered during Icon Composer setup that the supplied front, middle, and back PNG layers did not match the selected Sprout & Slice concept board. Continuing with those layers would produce a technically editable icon with the wrong geometry and appearance.

### Options considered

1. Keep and manually repair the three existing layers.
2. Generate three replacement layers from the concept.
3. Generate one complete transparent foreground that matches the concept, then control only its background in Icon Composer.

### Decision

Use option 3. `Fresh_App_Icon_Concept_02.png` is the authoritative visual reference. The next generator must reproduce its complete symbol as closely as possible in one `1024 × 1024` transparent PNG. The PNG contains no background or iOS mask. The owner configures background colors in Icon Composer.

The old three-layer assets are not production masters and are not committed as authoritative design sources. Runtime icon integration remained incomplete until the replacement PNG was reviewed and imported; DEC-012 records the accepted result.

### Consequences and revisit trigger

The exact approved geometry is easier to preserve and Icon Composer background changes remain flexible, while per-element depth control is intentionally sacrificed. Revisit only if Apple tooling requires multiple foreground layers or a verified single-layer export cannot preserve small-size readability.

---

## DEC-012 — Adopt the owner-finished Liquid Glass app icon

- Date: 2026-08-13
- Status: accepted
- Scope: visual identity, app icon, Xcode integration
- Related goal: G00 visual-foundation follow-up
- References: `Design/AppIcon/AppIcon_Foreground_Official.png`, `Fresh/AppIcon.icon`, `Design/AppIcon/APP_ICON_COMPOSER_SPEC.md`

### Context

Three regenerated single-foreground candidates were compared, and the owner selected artwork `3.png`. During Icon Composer setup, an initially light neutral background provided insufficient separation from the warm-white clock face. The owner finished the composition and changed the Default background to orange.

### Options considered

1. Keep a light neutral or sage background, preserving the earlier palette direction but weakening the clock boundary.
2. Use orange for Default, `System Dark` for Dark, and system-aware Tinted treatment.
3. Bake separate light, dark, and mono backgrounds into the PNG, reducing system adaptability.

### Decision

Use option 2. Preserve the selected `1230 × 1223` RGBA source byte-for-byte as `Design/AppIcon/AppIcon_Foreground_Official.png` and import it as one proportional foreground layer in `Fresh/AppIcon.icon`.

The saved Default fill is Icon Composer's automatic gradient seeded with orange `#FF8D28` (`extended-sRGB 1.0, 0.55294, 0.15686`); Dark uses `System Dark`. The group retains restrained neutral shadow and translucency (`0.5` each). Tinted/mono remains system-controlled, and its foreground glass specialization is disabled so recoloring retains recognizable clock, leaf, and tomato shapes. Default and Dark retain the Liquid Glass treatment.

The Xcode build setting already names `AppIcon`, so the `.icon` document is the runtime source. The earlier concept board remains historical guidance; it is no longer the production master.

### Consequences and revisit trigger

The orange field gives the warm-white clock a visible boundary while keeping the green leaves and orange-red tomato recognizable. Dark gains strong light-on-dark contrast, and Tinted can follow the user's system tint without a baked color dependency. Future visual-generation chats must treat the icon as final and must not repeat it as a generic screen illustration. Revisit only if an actual device check exposes poor legibility at a shipping icon size or a future Apple toolchain changes `.icon` behavior.

---

## DEC-013 — Generate UI screens sequentially with an asset-first visual handoff

- Date: 2026-08-13
- Status: accepted
- Scope: visual workflow, UI handoff, generated assets
- Related goal: visual preparation for G01 and later UI goals
- References: `Design/UI_SCREEN_GENERATION_PROMPTS.md`, `Fresh/Docs/VISUAL_GENERATION_GUIDE.md`, `Fresh/Docs/ScreenSpecs/`

### Context

The owner will use a separate image-generation chat to read the Fresh repository, generate each app page and its required transparent illustrations, and return detailed Markdown for later SwiftUI implementation. Generating everything in one request risks visual drift, lost context, inconsistent assets, and incomplete layout documentation.

### Options considered

1. One large prompt for all screens: fast to send, but difficult to review and likely to lose per-screen detail.
2. A new chat for every screen: isolated, but repeatedly loses component, data, and asset continuity.
3. One persistent chat with a style-lock prompt, one prompt per screen, asset-first generation, and a final cross-screen audit.

### Decision

Use option 3. Start with a repository-driven visual style lock, then generate Onboarding, Today, My Food, Quick Add, Estimate Review, Food Detail, Edit Food, and Settings in that order. For each page, generate reusable transparent artwork before composing mockups, reuse the same assets across every state, then write a standalone technical Markdown proposal with layout, typography, colors, contrast, SwiftUI mapping, states, and accessibility.

The final prompt audits navigation, exact copy, data continuity, reusable components, asset reuse, accessibility, and scope across all screens. The app icon remains identity rather than a repeated hero. Its orange background may inspire a limited warm accent, but it does not replace the warm off-white UI canvas or evergreen brand color.

### Consequences and revisit trigger

The process takes several generator turns but keeps feedback small and preserves a coherent system. Generated files remain proposals rather than source-of-truth changes until reviewed and accepted into the relevant screen specs. Revisit if the image tool cannot retain context or reliably reuse supplied assets; in that case, use the generated master handoff and asset manifest to seed a new chat instead of improvising a new style.

---

## DEC-014 — Apply proportional human-visible quality gates to generated UI assets

- Date: 2026-08-13
- Status: accepted
- Scope: visual QA, generated assets, reviewer workflow
- Related goal: visual preparation for G01 and later UI goals
- References: `Design/GeneratedUI/Proposals/FRESH_VISUAL_STYLE_LOCK.md`

### Context

Pixel-level inspection can identify genuine transparency failures, but repeatedly repairing artifacts that are invisible to people at the asset's actual UI size adds cost without improving the product. The owner wants good human-visible results, not microscopic perfection.

### Decision

Judge mockups at normal iPhone viewing size, food thumbnails at approximately `56–64 pt`, and detail heroes at approximately `180–220 pt`. Pixel sampling remains useful for validating alpha, contrast, or an artifact that is visible at the intended scale; invisible source-pixel irregularities are not blockers.

Do not enlarge a thumbnail into a detail hero merely because its source resolution permits it. Generate a dedicated hero asset when the larger composition needs one, and review that hero at its own usage size.

### Consequences and revisit trigger

Review cycles remain rigorous on copy, layout, contrast, scope, transparency, and visible consistency while avoiding diminishing-return polish. Revisit when an artifact becomes visible on a real target device, at an intended size, or on a supported Light/Dark background.

---

## DEC-015 — Keep one canonical visual mockup per screen

- Date: 2026-08-13
- Status: accepted
- Scope: visual workflow, feature specification, SwiftUI handoff
- Related goal: visual preparation for G01 and later UI goals
- References: `Design/GeneratedUI/Proposals/`, `Fresh/Docs/ScreenSpecs/`

### Context

Generating separate polished bitmaps for Light, Dark, empty, search-empty, Dynamic Type, and every intermediate state costs time and tokens while most differences are better expressed through native SwiftUI behavior. The owner prefers one clear design per page, with refinements made during coding.

### Options considered

1. Generate and review every visual state before implementation.
2. Generate one canonical screen per page and describe all alternate states and responsive behavior in Markdown.
3. Skip visual mockups and rely only on prose.

### Decision

Use option 2. Each screen has one canonical Light/default-content mockup that establishes hierarchy, component style, spacing, and visual continuity. Dark Mode, empty/error/loading, search/filter results, Dynamic Type, keyboard, validation, and unavailable states remain explicit Markdown acceptance criteria and are implemented and verified in SwiftUI.

Every canonical mockup must reflect the real feature contract: entry/exit, user inputs, system-generated values, persistence behavior, exact primary action, navigation destination, safety wording, and out-of-scope limits. Reviewers block only material concept, feature, copy, navigation, accessibility, contrast, or visible layout errors. Minor visual refinement is deferred to implementation.

A generated design may introduce a small native, reversible UX improvement that is absent from the current Markdown—such as a clear button, helpful disclosure, or better focus affordance—when it materially improves the same workflow. If accepted, record it in the proposal and reconcile the source spec before coding. It must not silently alter the feature's main purpose, input fields, required/optional semantics, user-versus-Fresh information ownership, persistence point, safety language, or navigation outcome. A proposal for a larger scope change remains a decision for the owner, not an automatic design addition.

Already-generated alternate-state images may remain as supplementary references and review history, but they are not competing canonical designs. Future agents must follow the file explicitly marked `Canonical` in each proposal.

### Consequences and revisit trigger

The handoff becomes smaller and easier to keep consistent while implementation remains responsible for real adaptive behavior. Revisit only when a materially different state cannot be communicated or evaluated safely through Markdown and native previews/tests.

---

## DEC-016 — Consolidate Quick Add into one scrollable form

- Date: 2026-08-13
- Status: accepted
- Scope: product flow, input UX, visual handoff
- Related goal: G05 Quick Add and Estimate Review
- References: `Fresh/Docs/ScreenSpecs/04_QUICK_ADD.md`, `docs/superpowers/specs/2026-08-13-quick-add-single-form-design.md`

### Context

The approved input model contains one required value and a small number of optional free-text/date inputs. A four-step wizard hides the total effort and adds navigation taps to a personal, lightweight capture flow. The owner asked whether all Quick Add inputs could live on one page.

### Options considered

1. Retain four steps: strong focus per question, but more taps and ceremony.
2. Use one long unstructured form: fewer taps, but weak hierarchy and unclear optional behavior.
3. Use one grouped, scrollable native sheet with a sticky `Tinjau estimasi` action.

### Decision

Use option 3. Show required `Nama bahan`, optional photo, free-text storage, free-text condition, free-text package status, reference-date choice, and collapsed additional details in one scrollable sheet. State clearly that the user may fill only what they know. Name remains the only required input; absent optional values remain unknown.

`Tinjau estimasi` preserves the draft and opens Estimate Review. It does not persist the food. Category and normalized values are still generated by Fresh and reviewed separately; deterministic rules remain the estimate source.

The previously approved four-step bitmap is preserved as superseded visual history. It no longer defines implementation.

### Consequences and revisit trigger

The form is faster and exposes its scope immediately, but keyboard avoidance, scrolling, field focus, and Dynamic Type need explicit implementation tests. Revisit only if usability testing shows the consolidated form is cognitively heavy or completion quality materially declines.
