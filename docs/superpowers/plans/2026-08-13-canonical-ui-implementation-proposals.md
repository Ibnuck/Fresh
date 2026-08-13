# Canonical UI Implementation Proposals Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Make the four approved canonical UI proposals precise enough that a new SwiftUI implementation chat does not need to infer layout, typography, color, interaction, or data ownership from bitmap pixels.

**Architecture:** Keep the screen specs authoritative and treat measurements as adaptive point-based intent. Each proposal uses the same implementation-handoff structure: canvas conventions, view tree, region geometry, typography, tokens, component contracts, interactions, state adaptations, accessibility, compliance, and deviations.

**Tech Stack:** Markdown, native SwiftUI design primitives, Dynamic Type, semantic colors, approved PNG references.

## Global Constraints

- Reference canvas is `402 × 874 pt`; generated pixels are not absolute implementation coordinates.
- Main horizontal inset is `20 pt`, spacing follows the `4 pt` grid, and interactive targets are at least `44 × 44 pt`.
- Use Dynamic Type and content-driven height; never shrink essential text to match the bitmap.
- One canonical visual per screen; alternate states remain implementation contracts.
- Screen spec overrides generated bitmap when they conflict.
- No feature, navigation, input-ownership, save-timing, or food-safety behavior changes.

---

### Task 1: Audit canonical contracts

**Files:**
- Read: `Fresh/Docs/DESIGN_SYSTEM.md`
- Read: `Fresh/Docs/ScreenSpecs/02_TODAY.md`
- Read: `Fresh/Docs/ScreenSpecs/03_MY_FOOD.md`
- Read: `Fresh/Docs/ScreenSpecs/04_QUICK_ADD.md`
- Read: `Fresh/Docs/ScreenSpecs/05_ESTIMATE_REVIEW.md`
- Read: `Design/GeneratedUI/Proposals/*.md`
- Inspect: four canonical PNGs

- [x] Map every canonical image to its authoritative screen spec and approved asset set.
- [x] Identify missing position, stack, frame, padding, spacing, typography, token, distribution, alignment, state, and accessibility details.

### Task 2: Complete My Food proposal

**Files:**
- Modify: `Design/GeneratedUI/Proposals/my-food_GENERATED_UI_PROPOSAL.md`

- [x] Add measurement conventions, full SwiftUI tree, region geometry, row/chip/search contracts, typography, tokens, interactions, states, accessibility, and compliance.
- [x] Preserve repaired Tempe runtime-asset guidance and superseded-image history.

### Task 3: Complete Quick Add proposal

**Files:**
- Modify: `Design/GeneratedUI/Proposals/quick-add_GENERATED_UI_PROPOSAL.md`

- [x] Define sheet/header/form/dock geometry, every field group, date-choice distribution, Dynamic Type typography, focus/keyboard/scroll behavior, validation, ownership, states, accessibility, and compliance.
- [x] Keep the single-form canonical decision and mark the wizard image as superseded.

### Task 4: Complete Estimate Review proposal

**Files:**
- Modify: `Design/GeneratedUI/Proposals/estimate-review_GENERATED_UI_PROPOSAL.md`

- [x] Define navigation, hero, provenance card, based-on rows, disclosure, adjustment, save dock, typography, tokens, state transitions, accessibility, and compliance.
- [x] Preserve the explicit unsaved-draft/persistence boundary and non-safety wording.

### Task 5: Normalize Today proposal

**Files:**
- Modify: `Design/GeneratedUI/Proposals/today_GENERATED_UI_PROPOSAL.md`

- [x] Add shared measurement conventions and any missing region/component details without replacing already reviewed values.
- [x] Confirm its structure and terminology match the other three proposals.

### Task 6: Verify and review

**Files:**
- Modify: `docs/PROJECT_JOURNAL.md`
- Modify if review exposes a source-contract defect: `Fresh/Docs/ScreenSpecs/04_QUICK_ADD.md`
- Modify if a durable interaction decision is required: `docs/decisions/DECISION_LOG.md`
- Review: the four canonical proposal Markdown files and their source specs/images.

- [x] Run heading/placeholder/path/hex/point-unit/diff checks.
- [x] Record the completed implementation handoff in the project journal.
- [x] Run a context-clean `$fresh-code-review` of the complete current documentation diff.
- [x] Repair valid findings and use a different fresh reviewer until the latest verdict is `Verdict: No material findings.`
- [x] Prepare owner-managed Git commit instructions; do not stage, commit, or push.
