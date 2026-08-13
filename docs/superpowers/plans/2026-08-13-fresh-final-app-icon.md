# Fresh Final App Icon Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Install the selected generated Sprout & Slice foreground as Fresh's final Liquid Glass app icon and make the decision durable across project documentation.

**Architecture:** Preserve the chosen RGBA PNG byte-for-byte under `Design/AppIcon/`, then import it as one proportional foreground layer into an official `Fresh/AppIcon.icon` document. Let Icon Composer own appearance backgrounds and system material rendering; keep runtime integration separate from repository-only design sources.

**Tech Stack:** Apple Icon Composer, Xcode 26.5 toolchain, `ictool`, iOS Simulator, Markdown.

## Global Constraints

- Do not stretch, crop, redraw, or split the selected artwork.
- Preserve the owner-finished appearance settings: an automatic orange gradient seeded with `#FF8D28` for Default and `System Dark` for Dark.
- Use system-aware Mono/Tinted treatment.
- Apply restrained Liquid Glass in Icon Composer, not in the PNG.
- Do not add third-party dependencies or modify Swift behavior.
- Codex must not stage, commit, push, or change Git configuration.

---

### Task 1: Preserve and inspect the official foreground

**Files:**
- Create: `Design/AppIcon/AppIcon_Foreground_Official.png`

**Interfaces:**
- Consumes: `/Users/ibnutaufickahraza/Downloads/desain app fresh/3.png`
- Produces: byte-identical repository master for Icon Composer and future visual chats

- [x] Copy the selected source to the repository master path without modifying the owner's original.
- [x] Compare source and repository SHA-256 values.
- [x] Verify dimensions, RGBA/alpha, and aspect ratio; record that proportional fitting is required.

### Task 2: Create the official Icon Composer document

**Files:**
- Create: `Fresh/AppIcon.icon`

**Interfaces:**
- Consumes: `Design/AppIcon/AppIcon_Foreground_Official.png`
- Produces: active Xcode app-icon source named `AppIcon`

- [x] Open Apple Icon Composer and create `Fresh/AppIcon.icon`.
- [x] Import the official master as one foreground layer and preserve its aspect ratio.
- [x] Save the owner's final Default orange automatic gradient (`#FF8D28`) and `System Dark` background.
- [x] Configure system-aware Mono/Tinted appearance without adding a background to the PNG.
- [x] Enable restrained Liquid Glass separation for Default/Dark and disable the foreground glass specialization for Tinted readability.
- [x] Inspect Default, Dark, and Mono/Tinted at large and small preview sizes, then save.

### Task 3: Verify icon exports and Xcode integration

**Files:**
- Verify: `Fresh/AppIcon.icon`
- Verify: `Fresh.xcodeproj/project.pbxproj`

**Interfaces:**
- Consumes: saved `.icon` document and existing `AppIcon` build setting
- Produces: export and build evidence

- [x] Use the bundled `ictool` to inspect help and export supported Default and non-default renditions to a temporary directory.
- [x] Confirm exported images are square, visually legible, and appearance-appropriate.
- [x] Discover current simulator destinations.
- [x] Run the full Fresh test action on an available iPhone simulator.
- [x] Inspect the built `.app` for compiled icon output and absence of loose design/Markdown sources.

### Task 4: Synchronize durable project memory

**Files:**
- Modify: `Design/README.md`
- Modify: `Design/AppIcon/APP_ICON_SPEC.md`
- Modify: `Design/AppIcon/APP_ICON_COMPOSER_SPEC.md`
- Modify: `Fresh/Docs/VISUAL_HANDOFF_README.md`
- Modify: `Fresh/Docs/DESIGN_SYSTEM.md`
- Modify: `docs/decisions/DECISION_LOG.md`
- Modify: `docs/PROJECT_JOURNAL.md`

**Interfaces:**
- Consumes: verified final icon configuration
- Produces: consistent project context for future coding and visual-generation chats

- [x] Record the selected master, actual dimensions, single-layer composition, background directions, and Liquid Glass boundary.
- [x] Add DEC-012 to both the decision-log index and full decision history.
- [x] Mark earlier regeneration/deferred language as historical or superseded where necessary.
- [x] Explain that screen illustrations share palette and organic character but must not repeat the app icon as a generic hero.

### Task 5: Quality gate and owner handoff

**Files:**
- Review: complete current working-tree diff

**Interfaces:**
- Consumes: implementation, export/build evidence, and documentation
- Produces: clean reviewer verdict and one Xcode commit subject for the owner

- [x] Run `git diff --check`, intended-scope inspection, ignored-file inspection, and likely-secret scans.
- [x] Run a context-clean `$fresh-code-review` reviewer; the first reviewer returned exactly `Verdict: No material findings.`
- [x] Validate the first review. No repair was required; a different context-clean final reviewer also returned exactly `Verdict: No material findings.`
- [x] Prepare the final commit message requested by the owner; do not perform Git writes.
