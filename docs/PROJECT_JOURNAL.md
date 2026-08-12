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
