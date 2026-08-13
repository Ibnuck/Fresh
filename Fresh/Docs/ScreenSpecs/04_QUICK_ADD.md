---
screen_id: quick-add
screen_name: Quick Add
platform: iOS
framework: SwiftUI
target_os_design_language: iOS 26
reference_device: iPhone portrait 402x874pt
appearance: Light Mode
content_state: single-form-default
status: approved-for-visual-generation
version: 3
---

# Quick Add

## 1. Outcome

Pengguna dapat mengisi seluruh informasi yang diketahui tentang satu bahan dalam satu sheet, lalu meninjau estimasi tanpa kehilangan data atau dipaksa memilih nilai palsu.

## 2. Presentation and flow

- Presented as one native large-detent sheet from global Add, Today empty CTA, or onboarding completion.
- One vertically scrollable form followed by Estimate Review; not a multi-step wizard.
- Name is required. Photo, storage, condition, package status, reference date, quantity, and notes are optional.
- Copy above optional fields: `Isi yang kamu tahu saja. Informasi yang kosong akan ditandai belum diketahui.`
- `Tinjau estimasi` preserves the draft and opens Estimate Review; it does not save.
- `Detail lainnya` is collapsed by default and does not obstruct the core form.

## 3. Top-to-bottom layout and exact copy

### Region A — Sheet header

- Native grabber when appropriate.
- Leading `Batal`; centered title `Tambah bahan`; no step counter.
- If the draft changed, cancel asks `Buang draft?` with `Lanjut mengisi` and destructive `Buang`.

### Region B — Introduction and name

- Main inset `20 pt`; content starts approximately `20–24 pt` below header.
- Headline `Tambahkan bahan dari dapurmu`.
- Supporting copy `Nama bahan wajib. Detail lainnya boleh dikosongkan dan ditambahkan nanti.`
- Large full-width text field with visible label `Nama bahan` and placeholder `Contoh: bayam atau susu segar`.
- Continuity value in canonical mockup: `Bayam`.
- Native clear button may appear while the field has text.
- Optional secondary `Tambah foto` with camera/photo icon. Photo is decorative identity only and not required for interpretation or estimation.

### Region C — Storage

- Section title `Penyimpanan`.
- Full-width free-text field with visible label `Lokasi penyimpanan`.
- Placeholder `Contoh: rak atas kulkas`; continuity value `Rak atas kulkas`.
- Fresh preserves the exact text and may normalize it internally when possible.

### Region D — Condition and package

- Section title `Kondisi saat ini`.
- First free-text field label `Kondisi bahan`; placeholder `Contoh: sudah dicuci dan dipotong`; continuity value `Sudah dicuci`.
- Second free-text field label `Status kemasan`; placeholder `Contoh: plastiknya sudah dibuka`; continuity value `Kemasan sudah dibuka`.
- Ripeness is not a separate field. If relevant, the user writes it naturally in `Kondisi bahan`, such as `alpukat masih keras`.
- Fresh preserves both raw strings and may normalize only details the user actually stated. Unstated condition, ripeness, or package state remains unknown.

### Region E — Reference date

- Section title `Tanggal acuan`.
- Supporting hint `Tanggal pada kemasan atau kapan bahan dibeli dapat membantu memperjelas estimasi.`
- Native single-selection choices: `Tanggal pada kemasan`, `Tanggal dibeli`, `Tidak ada tanggal`.
- Canonical continuity uses `Tanggal dibeli` and native date value `12 Agu 2026`.
- `Tidak ada tanggal` stores unknown and hides the date picker.

### Region F — Additional details

- Disclosure title `Detail lainnya`, collapsed by default.
- Expanded optional fields: quantity and notes only.
- Do not show price or store in MVP.

### Region G — Bottom action

- Keyboard-safe bottom dock with full-width primary `Tinjau estimasi`.
- Disabled only while trimmed `Nama bahan` is empty.
- Content scrolls so active fields and CTA are not hidden by the keyboard.

## 4. Information ownership

| Information | Owner/source | Rule |
|---|---|---|
| Name | User | Required; preserve raw string. |
| Photo | User | Optional/decorative, not an estimate requirement. |
| Storage | User free text | Preserve raw; normalize locally/optionally on-device. |
| Condition | User free text | Ripeness only when explicitly stated here. |
| Package status | User free text | Never guess an unstated state. |
| Reference type/date | User | May remain unknown. |
| Category | Fresh | Local catalog + optional Foundation Model; never a Quick Add field. |
| Normalized tags | Fresh | Derived only from stated text and shown at Estimate Review. |
| Freshness estimate | Deterministic Fresh rules | Foundation Model supplies no shelf-life or safety facts. |

## 5. Component inventory

| Component | SwiftUI mapping | Behavior |
|---|---|---|
| Sheet | `.sheet` + `NavigationStack` | Large detent; interactive dismissal follows draft policy. |
| Form | `ScrollView`/`Form` + grouped stacks | Content-driven height and keyboard scrolling. |
| Draft state | feature model | Persists across focus changes, validation, and Estimate Review back navigation. |
| Free-text input | `TextField` | Visible label, raw value preservation, no preset replacement. |
| Date choice/input | selection controls + `DatePicker` | Single reference type; conditional native date control. |
| Additional details | `DisclosureGroup` | Quantity and notes only; collapsed by default. |
| Bottom CTA | safe-area inset | Opens Estimate Review; never covered by keyboard. |

## 6. Error and edge states

- Blank name: CTA disabled; after attempted submit show `Masukkan nama bahan.` near the field.
- Save is not performed until Estimate Review confirmation.
- Smart interpretation unavailable: preserve raw text, use local matching where possible, and leave unresolved values unknown without a blocking AI banner.
- Dismiss accidental: preserve draft until discard is confirmed.
- Back from Estimate Review restores every value and focus-independent draft state.
- Large Dynamic Type: fields and date choices grow vertically; long controls are never side by side.
- Dark Mode: boundaries, labels, selection, and disabled state remain visible without relying on color alone.

## 7. Accessibility

- Every text field announces its visible label, current value, and concise hint.
- Optional fields communicate optional status; absence is not announced as an error.
- Validation is linked to `Nama bahan` and announced once after an attempted action.
- Photo button label describes the action, not only its icon.
- Date choices announce selected state.

## 8. Do not include

- Step progress, category picker, separate ripeness control, storage/condition/package preset rows, barcode/OCR scanner, AI chat, nutrition form, recipe categories, price/store fields, automatic save, or food-safety guarantees.

## 9. Requested output

- Canonical: `quick-add_form_light_v01.png`.
- Keyboard-focus, validation, Dark Mode, interpretation-unavailable, and Dynamic Type adaptations are specified in Markdown and verified during SwiftUI implementation; do not generate competing full-screen designs by default.
