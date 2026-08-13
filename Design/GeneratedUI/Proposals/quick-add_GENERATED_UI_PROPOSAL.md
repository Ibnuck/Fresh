---
proposal_for_screen: quick-add
proposal_version: 4
generator: Codex image generation
generated_at: 2026-08-13
source_spec_version: 4
approval_status: canonical-approved
---

# Generated UI Proposal — Quick Add

## Canonical assets and authority

| State | Image | Status |
|---|---|---|
| Single form, populated | `../Screens/quick-add_form_light_v01.png` | **Canonical** composition; final context-clean reviewer returned no material findings. |
| Superseded four-step candidate | `../Screens/quick-add_name-keyboard_light_v01.png` | Historical reference only; do not implement its `1 dari 4` or `Lanjut` flow. |

Implementation priority is: `Fresh/Docs/ScreenSpecs/04_QUICK_ADD.md` → `Fresh/Docs/DESIGN_SYSTEM.md` → this proposal → canonical bitmap. The bitmap fixes the accepted hierarchy and visual rhythm. Native safe areas, keyboard behavior, Dynamic Type, and the exact data contract take priority over pixel matching.

## Measurement conventions

- Reference viewport: `402 × 874 pt` iPhone portrait. The bitmap is a visual reference, not a fixed-coordinate specification.
- `Approx.` values may move by one `4 pt` spacing-grid step. `Minimum` values are accessibility constraints and must not shrink.
- Heights are content-driven unless explicitly marked otherwise; fields and rows grow vertically for wrapping text.
- Main horizontal content inset: `20 pt`; common gaps: `8, 12, 16, 20, 24 pt`.
- Respect the native sheet, navigation, keyboard, and home-indicator safe areas. Do not manually redraw system chrome.

## Feature and data contract

```text
Global Tambah / Today empty / Onboarding
└── Tambah bahan sheet (one scrollable form)
    ├── Nama bahan (required)
    ├── Tambah foto (optional/decorative)
    ├── Lokasi penyimpanan (optional free text)
    ├── Kondisi bahan (optional free text; includes ripeness when stated)
    ├── Status kemasan (optional free text)
    ├── Tanggal acuan (optional type and date)
    ├── Detail lainnya (collapsed: quantity and notes only)
    └── Tinjau estimasi
        └── Estimate Review; no persistence yet
```

Quick Add owns an unsaved draft. `Tinjau estimasi` preserves and passes that draft but never persists it. A changed draft requires discard confirmation. Only the trimmed name is required; every absent optional value remains unknown.

| Information | Source | Required? | Persistence/interpretation rule |
|---|---|---:|---|
| Name | User | Yes | Preserve raw string; trim only for empty validation. |
| Photo | User | No | Decorative identity only; never required for an estimate. |
| Storage | User free text | No | Preserve raw wording; optional local/on-device normalization. |
| Condition | User free text | No | Ripeness belongs here only when explicitly stated, for example `alpukat masih keras`. |
| Package status | User free text | No | Never infer an unstated open/closed state. |
| Reference type/date | User | No | May remain unknown; no hidden current-date default. |
| Quantity and notes | User | No | Available only inside `Detail lainnya`. |
| Category/normalized tags | Fresh | Not a field | Derived locally and optionally on-device; shown for review later. |
| Freshness estimate | Deterministic rules | Not a field | Foundation Model supplies no shelf-life or safety facts. |

## Canonical form content

| Group/control | Visible label or copy | Placeholder / canonical continuity value |
|---|---|---|
| Optional-data guidance | `Isi yang kamu tahu saja. Informasi yang kosong akan ditandai belum diketahui.` | Guidance only. |
| Introduction | `Tambahkan bahan dari dapurmu` | `Nama bahan wajib. Detail lainnya boleh dikosongkan dan ditambahkan nanti.` |
| Name | `Nama bahan` | `Contoh: bayam atau susu segar` / `Bayam`. |
| Photo action | `Tambah foto` | No image is required. |
| Storage section | `Penyimpanan` | Section heading. |
| Storage input | `Lokasi penyimpanan` | `Contoh: rak atas kulkas` / `Rak atas kulkas`. |
| Condition section | `Kondisi saat ini` | Section heading. |
| Condition input | `Kondisi bahan` | `Contoh: sudah dicuci dan dipotong` / `Sudah dicuci`. |
| Package input | `Status kemasan` | `Contoh: plastiknya sudah dibuka` / `Kemasan sudah dibuka`. |
| Date section | `Tanggal acuan` | `Tanggal pada kemasan atau kapan bahan dibeli dapat membantu memperjelas estimasi.` |
| Date choices | `Tanggal pada kemasan`; `Tanggal dibeli`; `Tidak ada tanggal` | Canonical selection: `Tanggal dibeli`; date: `12 Agu 2026`. |
| Disclosure | `Detail lainnya` | Collapsed; expands to quantity and notes only. |
| Primary action | `Tinjau estimasi` | Opens review; does not save. |

## Visual summary

The accepted screen is one calm, scrollable form rather than a wizard. The three-second hierarchy is `Tambah bahan` → required name → optional contextual fields → `Tinjau estimasi`. White input surfaces sit on the warm off-white canvas; evergreen identifies focus, selection, and the only dominant action. The page intentionally avoids category, preset, and AI-chat controls.

## SwiftUI view tree

```text
.sheet
└── NavigationStack
    ├── ScrollView
    │   └── LazyVStack(alignment: .leading, spacing: 20–24)
    │       ├── IntroGroup
    │       │   ├── Text("Tambahkan bahan dari dapurmu")
    │       │   └── Text("Nama bahan wajib…")
    │       ├── NameInput
    │       ├── AddPhotoButton
    │       ├── StorageSection
    │       │   └── LabeledTextField("Lokasi penyimpanan")
    │       ├── ConditionSection
    │       │   ├── LabeledTextField("Kondisi bahan")
    │       │   └── LabeledTextField("Status kemasan")
    │       ├── ReferenceDateSection
    │       │   ├── Text(hint)
    │       │   ├── SingleChoiceRows
    │       │   └── Conditional DatePicker
    │       └── DisclosureGroup("Detail lainnya")
    ├── toolbar
    │   ├── cancellationAction: Batal
    │   └── principal: Tambah bahan
    └── safeAreaInset(edge: .bottom)
        └── PrimaryButton("Tinjau estimasi")
```

Use one vertical scrolling owner. Keep draft state outside individual field views so focus changes and navigation to/from Estimate Review do not reset values.

## Region-by-region layout

| Region | Position and frame intent | Padding, spacing, alignment | Distribution | SwiftUI mapping and behavior |
|---|---|---|---|---|
| Sheet shell | Native large detent with system grabber; fills available portrait height | System top/bottom safe areas | Form owns flexible vertical space; dock remains outside its scroll area | `.sheet` + `NavigationStack`; interactive dismissal follows dirty-draft policy. |
| Header | Inline navigation height, content-driven; `Batal` target minimum `44 × 44 pt` | `Batal` leading; title optically centered; no trailing fake control | Leading action intrinsic; principal title centered independently | `ToolbarItem(.cancellationAction)` and `.principal`; title exact `Tambah bahan`. |
| Form content | Full available width below header | Horizontal `20 pt`; top approx. `20–24 pt`; bottom padding at least dock height + `16 pt` | One leading-aligned vertical column | `ScrollView` + `LazyVStack`; keyboard scrolls focused field into view. |
| Intro | Content-driven, full width | Headline/body gap `6–8 pt`; next control gap approx. `16–20 pt` | Both texts leading; body wraps | Headline + supporting text from the canonical form-content table. |
| Input surface | Full width; approx. `54–60 pt` at default size; radius `12 pt`; minimum tap height `44 pt` | Internal horizontal `16 pt`; vertical `10–12 pt`; visible label/value gap `2–4 pt` | Text entry expands; native clear button remains intrinsic | Reusable labeled `TextField`; subtle divider/border, visible focus state, no fake default. |
| Name group | First and visually strongest field | Error sits `4–8 pt` below field; photo action follows approx. `8–12 pt` later | Field full width; error leading | Required. Placeholder `Contoh: bayam atau susu segar`; canonical value `Bayam`. |
| Add photo | Content-driven row, minimum `44 pt` | Camera/photo icon then `8 pt` gap; leading aligned | Intrinsic, never full-width dominant CTA | Secondary `Button`; label `Tambah foto`; image remains optional/decorative. |
| Section title | Full width, content-driven | Approx. `20–24 pt` from previous group; `8–12 pt` to first field | Leading | `.headline`/semibold. Exact titles `Penyimpanan`, `Kondisi saat ini`, `Tanggal acuan`. |
| Condition pair | Two full-width fields stacked | Gap `12 pt`; never side-by-side | Equal available width, independent heights | `VStack`; long user text wraps or scrolls within native input behavior. |
| Date hint | Full width, content-driven | Approx. `6–8 pt` below title; `12 pt` before choices | Leading, wraps | `.subheadline` using exact hint. |
| Date choices | One grouped surface; each row minimum `48–52 pt` | Row horizontal `16 pt`; divider inset aligns with text; radio/value gap `12 pt` | Label flexible leading; selection mark intrinsic trailing/leading consistently | Single selection with native semantics. Exact choices: `Tanggal pada kemasan`, `Tanggal dibeli`, `Tidak ada tanggal`. |
| Date value | Appears only for dated selection; minimum `44 pt` | Approx. `8–12 pt` after choices | Label leading, value/control trailing; stacks vertically if needed | Native `DatePicker`; canonical value `12 Agu 2026`; no date UI for unknown. |
| Detail disclosure | Full width, minimum `52–56 pt`; radius `12–16 pt` if surfaced | Horizontal `16 pt`; chevron gap `8 pt` | Title flexible leading; chevron intrinsic trailing | `DisclosureGroup`, collapsed by default; expanded content contains quantity and notes only. |
| Bottom dock | Fixed to bottom safe area outside scroll; button approx. `50–54 pt`, radius `14–16 pt` | Dock top `10–12 pt`; horizontal `20 pt`; bottom system inset + visual breathing room | One full-width primary button | `.safeAreaInset(edge: .bottom)`; disabled only when trimmed name is empty; remains reachable above keyboard. |

## Typography

| Element | SwiftUI role | Weight/alignment | Adaptation |
|---|---|---|---|
| Navigation title | `.headline` | Semibold, centered | Native toolbar sizing. |
| Intro headline | `.title3` | Semibold, leading | Wraps; never scaled down. |
| Intro/date guidance | `.subheadline` | Regular, leading | Full-width multiline. |
| Section titles | `.headline` | Semibold, leading | Remain attached to following controls. |
| Field labels | `.caption` or `.subheadline` | Medium, leading | Must remain visible when populated. |
| Field values/placeholders | `.body` | Regular, leading | Dynamic Type and native text editing. |
| Choice labels | `.body` | Regular, leading | Each row grows vertically. |
| Validation | `.footnote` | Medium, leading | Linked to Name; announced once. |
| Primary button | `.headline` | Semibold, centered | Label never truncates. |

## Color, surface, and control tokens

| Role | Light direction | Dark direction | Usage/contrast rule |
|---|---|---|---|
| Canvas | `#F7F5EF` | `#111612` | Form background. |
| Surface | `#FFFFFF` | `#1B211D` | Fields, date group, disclosure, bottom dock material. |
| Primary text | `#18201B` | `#F3F5F1` | Titles and values. |
| Secondary text | `#667068` | `#AAB3AC` | Hints, labels, optional explanation. |
| Brand | `#1F6B4F` | `#5DBB8E` | CTA, focus, selected date choice. |
| Brand soft | `#DDEADF` | `#244232` | Selected/background emphasis only. |
| Divider | `#E4E5DF` | `#343B36` | Field/choice boundaries. |
| Validation | Semantic destructive red | Adaptive destructive red | Error text/icon; never color-only. |
| Disabled CTA | Reduced-emphasis brand/surface | Adaptive equivalent | Must still show disabled shape/label clearly. |

Normal text targets at least `4.5:1`. Prefer semantic/adaptive SwiftUI colors derived from these directions; verify actual output in Light, Dark, and Increase Contrast.

## Interaction and focus model

- Initial focus may enter `Nama bahan` when launched from an explicit Add action, but must not prevent the user seeing the header or dismiss controls.
- Return/Next advances through text fields; keyboard dismissal preserves every value.
- Native clear buttons and keyboard suggestions are platform affordances, not persisted Fresh features.
- Changing the reference choice updates the conditional DatePicker without inventing a value for `Tidak ada tanggal`.
- Name validates after field interaction: leaving the touched field empty or clearing an earlier value reveals the inline message; entering a nonempty trimmed value removes it.
- With a valid Name, `Tinjau estimasi` preserves the draft and opens Estimate Review. It never saves.
- Cancel/drag dismissal with changes asks `Buang draft?` with `Lanjut mengisi` and destructive `Buang`.

## State adaptations

| State | Required adaptation |
|---|---|
| Blank Name | CTA disabled. After the field has been touched, leaving it empty or clearing an earlier value shows `Masukkan nama bahan.` beside it; entering a nonempty trimmed value clears the message. This does not depend on activating a disabled button. |
| Unknown optional values | Leave fields empty; communicate optional status; do not substitute presets or hidden defaults. |
| No reference date | Select `Tidak ada tanggal`, hide DatePicker, store unknown. |
| Smart interpretation unavailable | Preserve raw text and continue silently with local matching/unknowns; no alarming AI banner. |
| Dirty dismissal | Present discard confirmation; keep form/draft if user continues. |
| Return from Estimate Review | Restore every value and disclosure state; no automatic persistence. |
| Keyboard visible | Focused control and dock remain reachable; scroll content does not disappear beneath keyboard. |
| Dynamic Type | Fields/choices grow vertically; labels and values may stack; dock label remains visible. |
| Dark/Increase Contrast | Preserve boundaries, focus, selection, and disabled distinction with adaptive tokens. |
| Reduce Motion | Date/disclosure changes use native reduced-motion behavior or short fade. |

## Accessibility annotations

VoiceOver order: `Batal` → `Tambah bahan` title → intro → Name → Name validation when present → Add photo → Storage heading/field → Condition heading/fields → Date heading/hint/choices/date → Detail disclosure → primary action.

- Every field exposes its visible label, current value, optional/required state, and concise hint.
- `Tambah foto` is an action label; its icon is hidden as a duplicate element.
- Date choices announce selected state and are separate minimum-44-point targets.
- Empty optional fields are `opsional, belum diisi`, not errors.
- `Tinjau estimasi` announces disabled state when Name is empty.
- Group section headings semantically without swallowing individual controls.

## Compliance matrix

| Requirement from source spec | Met? | Evidence/implementation contract |
|---|---|---|
| One form, not four steps | Yes | View tree, canonical asset, and obsolete candidate marker. |
| Exact required/optional inputs | Yes | Feature/data contract and region table. |
| Storage, condition, package are free text | Yes | Reusable labeled text fields; no presets. |
| Ripeness merged into condition | Yes | No separate control; preserve only explicit wording. |
| Category is Fresh-owned | Yes | Not present as an input; review occurs later. |
| Reference date can be unknown | Yes | Explicit `Tidak ada tanggal`, no hidden default. |
| Review does not save | Yes | CTA and draft contract. |
| Keyboard/draft/discard behavior | Yes | Focus model and state table. |
| Dynamic Type, VoiceOver, contrast | Yes | Adaptive layout, reading order, semantic tokens. |
| No prohibited feature | Yes | No category/ripeness preset, scanner, chat, price/store, nutrition, recipe, or auto-save. |

## Review history

1. The earlier candidate represented the now-superseded four-step flow and remains historical only.
2. Single-form v01 was generated and its bottom spacing repaired so `Detail lainnya` stays separate from the action dock.
3. A reviewer found a documentation contradiction in the adjacent prompt package; competing Estimate Review outputs were removed.
4. A different context-clean reviewer inspected the reconciled Quick Add/Estimate Review handoff and returned `Verdict: No material findings.`

## Assumptions and deviations

- The canonical image shows a populated, keyboard-dismissed continuity state so the whole contract fits in one frame; focus and keyboard avoidance are implementation requirements.
- Its outlined/labeled input styling may be implemented with native SwiftUI controls plus minimal decoration. Preserve hierarchy, labels, and contrast rather than reproducing every raster edge.
- Native radio/check, clear-field, disclosure, DatePicker, and camera affordances are accepted reversible details and add no persisted fields.

## Decisions needed

None outstanding. DEC-017 resolves the empty-name validation trigger.

## Suggested spec updates

None. This proposal adds implementation measurements without changing the approved product behavior.
