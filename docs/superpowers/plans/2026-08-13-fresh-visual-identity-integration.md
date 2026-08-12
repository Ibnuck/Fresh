# Fresh Visual Identity Reference Implementation Plan

**Goal:** Publish the approved visual references and the corrected one-layer icon decision before generating or integrating final artwork.

**Scope boundary:** Documentation and design references only. Do not modify Swift, the asset catalog, or create `Fresh/AppIcon.icon` in this goal.

## Task 1 — Preserve authoritative references

- [x] Store the selected icon concept at `Design/AppIcon/Fresh_App_Icon_Concept_02.png`.
- [x] Store the screen catalog at `Design/UIConcepts/fresh_ui_visual_direction.png`.
- [x] Verify dimensions and confirm both are reference boards rather than transparent runtime assets.

## Task 2 — Correct the icon specification

- [x] Record that the earlier front/middle/back layers do not match the selected concept.
- [x] Require one complete `1024 × 1024` transparent foreground PNG.
- [x] Require close visual reproduction rather than a loose reinterpretation.
- [x] Keep all background colors under owner control in Icon Composer.
- [x] Mark runtime integration as deferred.

## Task 3 — Reconcile the UI concept

- [x] Document the approved visual qualities.
- [x] Preserve official navigation, input, search, safety, and feature-scope decisions.
- [x] Add a clear source-of-truth order for future visual-generation work.

## Task 4 — Verification and publication gate

Before publication:

- check links, filenames, image metadata, and Markdown consistency;
- confirm the diff contains no app runtime changes or likely secrets;
- run a context-clean `$fresh-code-review` and repair valid findings;
- provide owner-managed staging, commit, and push instructions only after a clean verdict.

## Next goal after publication

Create the exact-generation prompt for one transparent icon foreground. Do not combine it with page mockups. After the owner returns an approved PNG, integrate it into `Fresh/AppIcon.icon`, configure backgrounds in Icon Composer, export renditions, build Fresh, and run a new review gate.
