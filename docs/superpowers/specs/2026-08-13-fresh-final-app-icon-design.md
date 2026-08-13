# Fresh Final App Icon Design

## Status

- Date: 2026-08-13
- Related goal: G00 visual-foundation follow-up
- Approval: approved in conversation
- Implementation state: completed and verified

## Outcome summary

Fresh uses the owner-selected generated artwork `3.png` as its official single-layer foreground in Apple Icon Composer, with appearance-aware backgrounds and restrained Liquid Glass treatment. The Xcode project builds the resulting `Fresh/AppIcon.icon`, while project Markdown records the final selection and its relationship to the broader visual system.

## Selected artwork

The authoritative source is `/Users/ibnutaufickahraza/Downloads/desain app fresh/3.png`. It contains the complete Sprout & Slice symbol on a transparent background and replaces the earlier concept board as the final foreground artwork.

Repository master: `Design/AppIcon/AppIcon_Foreground_Official.png`.

The supplied source is `1230 × 1223` RGBA. Preserve its aspect ratio and visible composition. Icon Composer may fit the artwork proportionally as one unit; never stretch it to force a square. The `.icon` document and exported runtime rendition provide the square system canvas.

## Icon Composer composition

- Document: `Fresh/AppIcon.icon`.
- Supported shapes: shared square rendition (used by Fresh on iOS and also available to macOS) plus the Icon Composer watchOS circle preview.
- Foreground: one transparent layer containing the complete icon.
- Light/Default background: Icon Composer automatic gradient seeded with orange `#FF8D28` (`extended-sRGB 1.0, 0.55294, 0.15686`). The owner selected orange after checking that a light neutral background collided with the warm-white clock face.
- Dark background: Icon Composer `System Dark`.
- Mono/Tinted: use Icon Composer's system-aware monochrome/tinted treatment instead of baking a custom color into the foreground.
- Keep the foreground geometry identical between appearances.

## Liquid Glass treatment

Liquid Glass is applied by Icon Composer and must not be rasterized into the PNG source.

- enable restrained specular/material response;
- use subtle depth/shadow separation;
- use the saved group-level neutral shadow and translucency treatment (`0.5` each) only while the symbol remains opaque and legible;
- avoid destructive blur, refraction, glow, or dramatic layer movement;
- prioritize recognition at small Home Screen sizes over visual intensity.

The foreground's tinted specialization disables its own glass treatment. This preserves shape contrast when iOS recolors the icon, while Default and Dark retain the Liquid Glass depth treatment.

The selected foreground already contains illustration highlights. System material effects must complement those highlights, not double them or make the icon glossy enough to lose its flat-organic identity.

## Runtime integration

The existing build setting `ASSETCATALOG_COMPILER_APPICON_NAME = AppIcon` matches the Icon Composer document name. `Fresh/AppIcon.icon` lives inside the synchronized Fresh group and becomes the active icon source in supported Xcode builds. The existing empty `AppIcon.appiconset` remains a reversible project fallback and is not populated with the non-square source artwork.

## Documentation memory

Update these durable sources after successful integration:

- `Design/README.md` — identifies the official master and active `.icon` document;
- `Design/AppIcon/APP_ICON_SPEC.md` — final artwork status and file properties;
- `Design/AppIcon/APP_ICON_COMPOSER_SPEC.md` — final appearance and Liquid Glass settings;
- `Fresh/Docs/VISUAL_HANDOFF_README.md` — tells future visual chats that the icon is final;
- `Fresh/Docs/DESIGN_SYSTEM.md` — connects screen illustrations to the final icon without copying it into every screen;
- `docs/decisions/DECISION_LOG.md` — records final artwork and appearance selection;
- `docs/PROJECT_JOURNAL.md` — summarizes integration and verification.

## Verification

- source and repository master match by SHA-256;
- Icon Composer saves a valid `Fresh/AppIcon.icon` with one foreground layer;
- `ictool` exports Default and at least one non-default rendition at `1024 × 1024`;
- exported renditions are visually inspected for Light, Dark, and Mono/Tinted behavior;
- Fresh builds and tests on a discovered iOS Simulator destination without app-icon errors;
- built `Fresh.app` contains compiled icon output but no loose design master, concept board, or Markdown;
- current Git diff contains only intended project files and no likely secrets;
- latest context-clean reviewer returns exactly `Verdict: No material findings.`

## Acceptance criteria

- The owner-selected foreground is the active Fresh application icon.
- Default orange separates the warm-white clock from its background; Dark preserves strong light-on-dark separation.
- Mono/Tinted remains readable through system treatment and silhouette.
- Liquid Glass is visible but restrained and does not obscure the clock, leaves, or tomato.
- All relevant Markdown consistently describes the icon as final and integrated.
- No Git write is performed by Codex; the owner receives only the final Xcode commit message after the quality gate.
