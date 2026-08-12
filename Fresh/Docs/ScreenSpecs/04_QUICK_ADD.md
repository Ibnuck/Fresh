---
screen_id: quick-add
screen_name: Quick Add
platform: iOS
framework: SwiftUI
target_os_design_language: iOS 26
reference_device: iPhone portrait 402x874pt
appearance: Light Mode
content_state: step-1-default
status: approved-for-visual-generation
version: 2
---

# Quick Add

## 1. Outcome

Pengguna dapat membuat draft bahan dengan beban input rendah, tanpa kehilangan data atau dipaksa memilih nilai palsu saat belum tahu jawabannya.

## 2. Presentation and flow

- Presented as native sheet from global Add/CTA.
- Medium detent dapat dipakai untuk step nama; expand large saat keyboard/detail perlu ruang.
- Four input steps followed by Estimate Review:
  1. Nama.
  2. Lokasi penyimpanan dalam teks bebas.
  3. Kondisi bahan dan status kemasan dalam teks bebas.
  4. Tanggal acuan.
- `More Details` tersedia tetapi collapsed dan tidak menghalangi primary flow.

## 3. Shared sheet chrome

### Region A — Sheet header

- Grabber native bila appropriate.
- Leading `Batal`; center title `Tambah bahan`; trailing text progress `1 dari 4`.
- Batal saat draft berubah memunculkan confirmation: `Buang draft?`, actions `Lanjut mengisi` dan destructive `Buang`.

### Region B — Question

- Inset 20 pt, approx. 20–24 pt below header.
- Headline satu pertanyaan; supporting hint di bawah.
- Input atau pilihan tanggal dimulai 20 pt setelah hint.

### Region C — Bottom action

- Primary full-width `Lanjut`; disabled hanya ketika nama kosong pada step 1.
- Secondary `Lewati untuk sekarang` pada optional steps 2–4; menyimpan `unknown`.
- Keyboard safe-area inset; CTA tidak tertutup keyboard.

## 4. Step details and exact copy

### Step 1 — Name

- Headline `Apa yang ingin kamu tambahkan?`
- Hint `Mulai dengan nama sederhana, misalnya bayam atau susu segar.`
- Large native text field label/placeholder `Nama bahan`.
- Example typed value: `Bayam` with focus ring/cursor.
- Optional photo button `Tambah foto` below input, secondary style; photo is never required.
- CTA `Lanjut`.

### Step 2 — Storage

- Headline `Disimpan di mana?`
- Hint `Tulis dengan bahasamu sendiri, misalnya rak atas kulkas atau meja dapur.`
- One full-width native text field with visible label `Lokasi penyimpanan` and placeholder `Contoh: rak atas kulkas`.
- Example typed value for continuity: `Rak atas kulkas`.
- Fresh preserves the exact text and interprets it internally as a normalized storage method when possible.
- Secondary `Belum tahu` or `Lewati untuk sekarang`; prefer one phrase consistently—mockup uses `Lewati untuk sekarang`.

### Step 3 — Condition

- Headline `Bagaimana kondisinya?`
- Hint `Ceritakan kondisi bahan dan kemasannya secara singkat. Kamu dapat mengubahnya nanti.`
- First full-width native text field:
  - visible label `Kondisi bahan`;
  - placeholder `Contoh: sudah dicuci dan dipotong`;
  - continuity value `Sudah dicuci`.
- Tingkat kematangan bukan field tersendiri. Jika relevan, pengguna menuliskannya secara natural di sini, misalnya `alpukat masih keras` atau `pisang sudah sangat matang`.
- Second full-width native text field:
  - visible label `Status kemasan`;
  - placeholder `Contoh: plastiknya sudah dibuka`;
  - continuity value `Kemasan sudah dibuka`.
- Fresh preserves both original texts and may normalize stated details into internal condition/package tags. Details not stated remain `unknown`; no ripeness or package state is guessed.

### Step 4 — Reference date

- Headline `Ada tanggal acuan?`
- Hint `Tanggal pada kemasan atau kapan bahan dibeli membantu memperjelas estimasi.`
- Choices: `Tanggal pada kemasan`, `Tanggal dibeli`, `Tidak ada tanggal`.
- If date choice selected, show native date field. Continuity example: `Tanggal dibeli`, `12 Agu 2026`.
- CTA exact `Tinjau estimasi`.

### More Details

- Disclosure title `Detail lainnya`.
- Collapsed by default. Expanded optional fields: quantity, notes; do not show price/store in MVP visual.

## 5. Component inventory

| Component | SwiftUI mapping | Behavior |
|---|---|---|
| Sheet | `.sheet` + `NavigationStack` | Detent changes with content/keyboard. |
| Step state | feature model | Draft persists across steps and validation errors. |
| Free-text input | `TextField` | Preserves user wording; visible label and example placeholder. |
| Date choice/input | `Button`, `DatePicker` | Selects reference type and uses native date UI. |
| Bottom CTA | safe-area inset | Never covered by keyboard. |

## 6. Error and edge states

- Name blank: CTA disabled; after attempted submit show `Masukkan nama bahan.` near field.
- Save is not performed in Quick Add until Estimate Review confirmation.
- Smart interpretation unavailable: no blocking banner; preserve the raw text, use local matching where possible, and leave unresolved values `unknown`.
- Dismiss accidental: preserve draft until confirmed discard.
- Large Dynamic Type: fields and date choices grow vertically; do not put two long controls side by side.
- Dark Mode: text-field boundaries, labels, and selected date choice remain clearly visible without relying on color alone.

## 7. Accessibility

- Progress announces `Langkah 1 dari 4`.
- Every text field announces its visible label, current value, and concise hint.
- Error message linked to field and announced after submit attempt.
- Photo button label describes action, not icon.

## 8. Do not include

- Category picker, separate ripeness control, storage/condition/package preset rows, barcode/OCR scanner, AI chat, nutrition form, recipe categories, price/store fields in default view, or every field on one long form.

## 9. Requested outputs

- `quick-add_name-keyboard_light_v01.png`
- `quick-add_storage_light_v01.png`
- `quick-add_condition_light_v01.png`
- `quick-add_date_light_v01.png`
