---
proposal_for_screen: quick-add
proposal_version: 2
generator: Codex image generation
generated_at: 2026-08-13
source_spec_version: 3
approval_status: canonical-approved
---

# Generated UI Proposal — Quick Add

## Outputs

| State | Image | Status |
|---|---|---|
| Single form, populated | `../Screens/quick-add_form_light_v01.png` | **Canonical approved; final context-clean reviewer returned no material findings.** |
| Superseded four-step candidate | `../Screens/quick-add_name-keyboard_light_v01.png` | Historical reference only; do not implement. Its `1 dari 4` and `Lanjut` flow is obsolete. |

## Feature contract

```text
Global Tambah / Today empty / Onboarding
└── Tambah bahan sheet (one scrollable form)
    ├── Nama bahan (required)
    ├── Tambah foto (optional/decorative)
    ├── Lokasi penyimpanan (optional free text)
    ├── Kondisi bahan (optional free text)
    ├── Status kemasan (optional free text)
    ├── Reference type/date (optional)
    ├── Detail lainnya (collapsed: quantity, notes)
    └── Tinjau estimasi
        └── Explicit Simpan bahan → Today/My Food
```

Quick Add owns an unsaved draft. `Tinjau estimasi` never persists it. A modified draft requires discard confirmation. Only the trimmed name is required; every absent optional value remains unknown.

## Information ownership

| Information | Source | Behavior |
|---|---|---|
| Name | User | Required and preserved exactly. |
| Photo | User | Optional visual identity only. |
| Storage, condition, package | User free text | Raw wording preserved; may be normalized only when stated. |
| Ripeness | User condition text only | Never a separate field or inferred value. |
| Reference date/type | User | May remain unknown. |
| Category and normalized tags | Fresh | Local matching + optional on-device interpretation; reviewable on Estimate Review. |
| Estimate | Deterministic rules | Foundation Model supplies no shelf-life/safety facts. |

## Canonical layout intent

- Native large-detent sheet with grabber, `Batal`, and centered `Tambah bahan`; no progress counter and no app tabs.
- `20 pt` main inset; vertically grouped form with one-level functional surfaces and visible labels.
- Intro makes required/optional behavior explicit.
- Reference-date choices are vertical/native and reveal a DatePicker only when relevant.
- `Detail lainnya` remains collapsed.
- Sticky safe-area `Tinjau estimasi`, approximately `50–54 pt`, stays above the keyboard; scroll keeps focused fields visible.
- Normal text uses Dynamic Type roles and target contrast `4.5:1`; targets are at least `44 × 44 pt`.

## Interaction, errors, and accessibility

- Native clear buttons and keyboard suggestions are accepted platform affordances, not persisted Fresh features.
- Blank name links `Masukkan nama bahan.` to the field; the CTA remains disabled.
- Cancel with changes asks `Buang draft?`; Estimate Review back restores all values.
- Interpretation unavailable is silent/non-blocking; raw text survives.
- VoiceOver receives visible labels, values, optional/selected state, validation, and action-oriented icon labels.
- Dynamic Type grows the form vertically. Dark/Increase Contrast use semantic adaptive tokens.

## Scope and implementation source

Do not implement the superseded step counter, `Lanjut`, storage/condition/package presets, category/ripeness fields, barcode/OCR, AI chat, price/store, auto-save, or safety guarantee. The source screen spec remains authoritative; this proposal supplies the canonical composition.

## Visual notes

- The image shows a populated, keyboard-dismissed state so the whole information contract can be reviewed in one frame. Keyboard avoidance/focus remains an implementation requirement, not a second canonical design.
- The generated form uses native clear-field, radio/check selection, date-row disclosure, and camera affordances. They do not introduce new persisted fields.
- `Detail lainnya` and the primary dock are visibly separate; in SwiftUI, form content must receive bottom safe-area padding so this remains true while scrolling.

## Review history

1. The earlier canonical candidate represented the now-superseded four-step flow and remains historical only.
2. The single-form v01 composition was generated, then its bottom spacing was repaired before project integration so `Detail lainnya` remains visibly separate from the action dock.
3. The first integrated reviewer found one documentation contradiction: Prompt 05 still requested competing Estimate Review state bitmaps.
4. The prompt package and adjacent screen-output contracts were reconciled to the one-canonical rule.
5. A different context-clean reviewer inspected the complete Quick Add/Estimate Review handoff and returned `Verdict: No material findings.`
