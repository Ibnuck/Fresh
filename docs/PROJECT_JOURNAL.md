# Fresh Project Journal

## 2026-08-12 — From starter app to an agent-ready project

### Starting point

Fresh began as a default SwiftUI starter app with `Hello, world!`, placeholder unit/UI tests, an Xcode project targeting iOS 26.5, and two substantial research documents covering the product concept and UI/UX direction.

### What we discussed

The owner wanted agentic engineering—loops, agents, specs, skills, optional plugins, clear goals, and repeated independent review—but explicitly did not want a complex enterprise framework. The app pages also needed enough written detail for a separate image-generation chat to create mockups and return a Markdown proposal.

A web visual companion was briefly explored. It did not fit the desired workflow, so it was removed from the project and replaced with Markdown-first visual specifications.

### How brainstorming worked

1. Read existing project research and inspect the starter code/project settings.
2. Research official Codex guidance and adjacent agent practices.
3. Compare minimal, lightweight, and full-framework approaches.
4. Present architecture, feature scope, reviewer loop, and visual documentation in sections.
5. Receive user approval, then write the durable design spec.
6. Incorporate later constraints: goal summaries, detailed `.gitignore`, Swift skills, QA/QC skill, Git policy, and decision memory.

### What was created

- Lightweight agentic design and G00 implementation plan.
- `AGENTS.md`, project Codex config, and read-only reviewer role.
- G00–G10 roadmap with outcome summaries and feature branch names.
- Architecture, workflow, review records, and detailed Xcode/Swift `.gitignore`.
- Four audited Swift skills and two pressure-tested Fresh quality-gate skills.
- Standalone visual handoff, design system, generator guide, templates, and eight MVP screen specs.
- Decision log and reusable project playbook.

### How skill choices were validated

Skills were not added simply because they sounded useful. Context-clean sub-agents were first tested without custom guidance. The review and Git baselines exposed consistency/publication problems, so custom skills were written and forward-tested five times. A proposed feature-cycle skill was omitted because fresh agents already followed the full workflow from the repo docs.

### Quality and Git state

The unchanged starter app built and all starter tests passed on an available iPhone 17 Pro simulator. Documentation under `Fresh/Docs` was excluded from target membership after build output showed it would otherwise be copied into the app bundle. The first context-clean full-tree review returned no material findings; a second final-tree check follows the creation of the durable review record.

The planned first commit is `chore: establish Fresh agentic project foundation`. Local `origin` currently points to `https://github.com/Ibnuck/Fresh.git`, but authenticated repository/visibility/history verification remains required before publication.

### What comes next

1. Finish G00 validation and fresh final review.
2. Review the written product/agentic design with the owner.
3. Commit/push G00 only after a clean gate.
4. Create `dev` and begin G01 App Shell on `feature/g01-app-shell`.
5. Before coding each UI goal, incorporate approved Markdown feedback from the external image-generation chat into the relevant source screen spec.

## 2026-08-13 — Git ownership clarified

The owner manually committed and pushed the G00 baseline through Xcode as `bf7e711` (`init: project agent markdown`). Local `main` and `origin/main` were observed at the same commit, with all 105 intended files tracked, no non-ignored untracked files, and DEC-009/free-text Quick Add included.

After this experience, the owner chose a permanent manual Git boundary. Codex now performs only read-only Git inspection and provides a complete post-gate handoff: branch/base, exact paths, commit subject, commands, push target, PR text, and expected checks. The owner performs every branch, staging, commit, push, PR, merge, authentication, and configuration action.

## 2026-08-13 — Visual reference corrected before icon generation

The selected Sprout & Slice concept board and the UI visual catalog were added as project references. During the first Icon Composer attempt, the owner noticed that the supplied three foreground layers did not match the selected icon concept. The project therefore stopped before claiming a runtime icon.

The corrected direction uses one complete transparent foreground PNG that must reproduce the concept as closely as possible. Background colors remain under owner control in Icon Composer. This reference milestone is published first; the exact image-generation prompt and runtime integration follow as separate reviewed steps.

## 2026-08-13 — Final Liquid Glass app icon selected and integrated

The owner compared three regenerated single-foreground candidates and selected `3.png` as the official Sprout & Slice artwork. The source was preserved unchanged in `Design/AppIcon/AppIcon_Foreground_Official.png` and imported as one proportional layer into `Fresh/AppIcon.icon`; the copy inside the Icon Composer document is byte-identical to the repository master.

During visual review, a light neutral background was found to collide with the warm-white clock. The owner finalized Default with an orange automatic gradient seeded at `#FF8D28`, kept Dark on Icon Composer's `System Dark`, and retained system-controlled Tinted behavior. Default and Dark use restrained Liquid Glass depth; the Tinted foreground disables its glass specialization so the silhouette remains readable when recolored.

Official `ictool` exports for Default, Dark, Tinted Light, and Tinted Dark were generated at `1024 × 1024` and inspected. Default separates the clock from the background, Dark has strong contrast, and tinted renditions retain the clock–leaves–tomato structure. Build/test and the context-clean reviewer gate are completed before the owner receives the Xcode commit message.

The full Xcode test action passed seven test invocations on an iPhone 17 Pro simulator. Two completed context-clean reviewers independently returned `Verdict: No material findings.` after inspecting the final icon sources, appearance exports, compiled asset stacks, bundle contents, documentation, and verification evidence. A reviewer process that stalled during a reconnect was interrupted and not counted as a quality verdict.

## 2026-08-13 — Sequential UI generation handoff prepared

The visual-generation workflow was converted into a copy-paste prompt sequence for one persistent external chat. It begins with a repository-based style lock, continues through the eight approved screen specs one at a time, requests only the transparent illustrations each screen needs, and finishes with a cross-screen audit and master handoff.

Each page prompt asks the generator to create reusable assets before mockups, reuse those exact assets across screen states, and write standalone Markdown containing SwiftUI hierarchy, approximate layout measurements, Dynamic Type roles, Light/Dark hex tokens and contrast pairings, interaction states, accessibility, compliance, and deviations. The sequence preserves Fresh's product decisions: search only in My Food, generated category, free-text storage/condition/package, no separate or inferred ripeness, user-selected reference date, decorative photos, and no safety guarantees or out-of-scope features.

Generated-asset review was later calibrated to human-visible use rather than microscopic perfection. Mockups are judged at normal iPhone scale, thumbnails at `56–64 pt`, and hero art at `180–220 pt`. Pixel inspection is reserved for transparency, contrast, or artifacts visible at the intended size; thumbnails are not enlarged into detail heroes.

The owner then simplified the handoff to one canonical visual mockup per page. Alternate appearances and interaction states remain detailed Markdown contracts and will be implemented and verified in native SwiftUI. Canonical review now checks the real feature workflow—including user-entered versus generated information, persistence/navigation outcomes, accessibility, safety wording, and scope—not only visual polish.

Generated proposals may contribute small useful native affordances even when the source spec did not name them, as long as they are documented and do not change the main feature flow or what information is entered. Larger scope changes remain explicit product decisions.

## 2026-08-13 — Canonical Today, My Food, Quick Add, and Estimate Review visuals

Codex generated and context-clean reviewed the first canonical UI handoffs using the final Sprout & Slice palette: Today populated Light, My Food populated Light, Quick Add, and Estimate Review. Supplementary Today empty/Dark and My Food search-empty images remain useful state references, but each page still has only one canonical implementation anchor. Reusable transparent Bayam, Susu, Tempe, Alpukat, and Today empty-container assets live under `Design/GeneratedUI/Illustrations/`.

The owner replaced the earlier four-step Quick Add direction with one grouped, scrollable form. The final canonical file is `Design/GeneratedUI/Screens/quick-add_form_light_v01.png`; `quick-add_name-keyboard_light_v01.png` remains superseded history. The form preserves exactly the same information model: required name, optional decorative photo, free-text storage, free-text condition, free-text package status, optional reference date, and collapsed quantity/notes. `Tinjau estimasi` opens the review screen without saving.

Estimate Review's canonical file is `Design/GeneratedUI/Screens/estimate-review_available_light_v01.png`. It visibly distinguishes user text, `Interpretasi Fresh`, deterministic-rule provenance, confidence, the non-safety disclaimer, and the explicit first save action. Its context-clean reviewer returned `Verdict: No material findings.`

The integrated Quick Add/Estimate Review gate required two reviewer cycles. The first found that the active Estimate Review generation prompt still requested multiple competing state bitmaps. After reconciling Prompt 05 and adjacent future-screen output contracts with DEC-015, a different context-clean reviewer returned `Verdict: No material findings.` No runtime Swift/Xcode behavior changed in this design-only handoff.

## 2026-08-13 — Tempe thumbnail alpha repaired

The first transparent Tempe export had visible holes in its cream-white soybean/mycelium texture because the chroma-removal algorithm treated some internal light pixels as background. The intact magenta-source image was reprocessed conservatively: background removal is now limited to saturated magenta pixels connected to the outer canvas border. The project keeps the same asset path, `Design/GeneratedUI/Illustrations/food_thumbnail_tempe_transparent.png`, so future My Food implementation automatically consumes the repaired image. It is scoped to `48–64 pt` row usage and was checked on Fresh Light and Dark surfaces at `64 pt`.

## 2026-08-13 — Canonical UI implementation proposals completed

The approved Today, My Food, Quick Add, and Estimate Review visuals now each have a standalone implementation proposal detailed enough for a new SwiftUI coding chat to work without measuring the PNG or reconstructing decisions from conversation history. Every proposal records its authoritative source order, adaptive `402 × 874 pt` reference canvas, SwiftUI view tree, region geometry, padding/spacing/alignment/distribution, typography roles, Light/Dark token directions, component or field contracts, interactions, alternate states, VoiceOver order, compliance, and deviations.

Measurements deliberately describe point-based intent rather than rigid screenshot coordinates. Approximate dimensions may move by one spacing-grid step; minimum hit targets and accessibility constraints may not shrink; content grows for Dynamic Type. The screen specs remain authoritative over generated pixels, and each screen keeps one canonical bitmap while alternate state images remain supplementary references.

The handoff preserves the product boundaries already approved: search exists only in My Food; Quick Add remains one form with user-entered free-text storage, condition, and package status; ripeness is not a separate field; category/normalization is Fresh-owned and reviewable; `Tinjau estimasi` does not save; only successful `Simpan bahan` persists; and freshness wording never promises food safety.

The first context-clean implementation-proposal review found three cross-document defects: two Today copy/token gaps and an unreachable Quick Add validation trigger. Today was reconciled to the exact approved metadata/suggestion and received explicit Dark token directions. Quick Add keeps its empty-name disabled CTA, but its inline validation now appears after the Name field has been touched and then left/cleared empty; it no longer depends on tapping a disabled control. DEC-017 records that interaction rule.

The second context-clean review found that some Today and My Food alternate-state copy was referenced as exact but not repeated in the standalone proposals. The approved Today context/empty copy and My Food search-empty template were copied from their authoritative screen specs so a future implementation chat does not need to infer or transcribe them.

The third context-clean review found the same omission pattern in Estimate Review's Needs Review state. Its full approved unresolved-storage explanation was copied from the source spec into the proposal, including the user-entered `dekat jendela` phrase and both recovery actions.

After a literal source-to-proposal copy audit closed the remaining My Food entry/search template and Quick Add example wording, a fourth context-clean reviewer inspected the complete documentation and visual handoff and returned `Verdict: No material findings.` Swift build/tests were not applicable because this goal changes no runtime code, project setting, or compiled asset.
