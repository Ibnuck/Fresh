---
screen_id: edit-food
screen_name: Edit Food
platform: iOS
framework: SwiftUI
target_os_design_language: iOS 26
reference_device: iPhone portrait 402x874pt
appearance: Light Mode
content_state: existing-item
status: approved-for-visual-generation
version: 2
---

# Edit Food

## 1. Outcome

Pengguna dapat memperbaiki data bahan dengan memahami field mana yang akan mengubah estimasi dan tanpa kehilangan perubahan saat save gagal.

## 2. Entry, exit, and primary action

- Entry: `Edit` from Food Detail.
- Presentation: native sheet or pushed form; use sheet with NavigationStack for visual continuity.
- Primary: `Simpan` in trailing navigation or bottom dock; choose bottom full-width for consistency with creation form.
- Secondary: `Batal` leading.
- Exit: successful save returns to updated Food Detail.

## 3. Three-second hierarchy

1. Title `Edit Bayam`.
2. Fields affecting estimate grouped first.
3. Info note `Perubahan pada bagian ini akan menghitung ulang estimasi.`
4. Additional fields grouped separately.
5. Save CTA.

## 4. Top-to-bottom layout

### Region A — Navigation

- Inline title `Edit Bayam`, leading `Batal`.
- If unsaved changes and Cancel tapped: `Buang perubahan?` confirmation.

### Region B — Estimate inputs group

- Group header `Mempengaruhi estimasi`.
- Small sage/slate info line with refresh icon: `Perubahan pada nama, kondisi, penyimpanan, kemasan, atau tanggal akan menghitung ulang estimasi.`
- Form rows in order:
  - `Nama bahan` → `Bayam` text field.
  - `Lokasi penyimpanan` → `Rak atas kulkas` text field.
  - `Kondisi bahan` → `Sudah dicuci` text field.
  - `Status kemasan` → `Kemasan sudah dibuka` text field.
  - `Tanggal acuan` → `Dibeli • 12 Agu 2026`.
- Use visible labels; no placeholder-only form.
- Do not add a category or ripeness field. The current generated category may appear as a read-only `Interpretasi Fresh: Sayuran berdaun` note and is confirmed/corrected in Estimate Review when recomputation occurs.

### Region C — Other details group

- Header `Detail lainnya`.
- Rows:
  - `Foto` → thumbnail + `Ubah`.
  - `Catatan` → `Tidak ada catatan`.
- Caption: `Mengubah bagian ini tidak menghitung ulang estimasi.`

### Region D — Current estimate preview

- Compact surface near bottom, not full Estimate Review duplication.
- `Estimasi saat ini` → `Gunakan hari ini • Hari ini`.
- If affecting field changes, state becomes `Estimasi akan diperbarui setelah ditinjau` with refresh icon.

### Region E — Save dock

- Primary `Tinjau perubahan` when recompute-affecting fields changed; destination Estimate Review.
- Primary `Simpan` when only other details changed.
- Button disabled when no changes or required name empty.

## 5. Interaction rules

- Do not recompute on photo/note changes.
- Recompute after name/condition/storage/package/date changes; those changes may also produce a new generated category. The user reviews the interpretation before final save.
- Preserve all edits on validation, recompute, or persistence error.
- Save error inline above CTA: `Perubahan belum tersimpan. Coba lagi.`
- Avoid autosave that makes Cancel meaningless.

## 6. Component inventory

| Component | SwiftUI mapping | Behavior |
|---|---|---|
| Grouped form | `Form`/`List` sections | Native scrolling and keyboard behavior. |
| Free-text rows | `TextField` | Preserve exact user wording and support keyboard navigation. |
| Note | semantic info label | Explains recompute, not decorative. |
| Estimate preview | compact card | Updates to pending state. |
| Save | safe-area button | Routes through review or persists. |

## 7. States

- No changes: CTA disabled.
- Validation: `Nama bahan tidak boleh kosong.` beneath/near field.
- Recompute needed: preview changes to pending.
- Save failure: draft retained.
- Large Dynamic Type: labeled rows become vertical where needed.
- Dark Mode: grouped form uses native surfaces, no low-contrast gray-on-gray.

## 8. Accessibility

- Each row announces label and current value.
- Recompute info is announced before affected fields or as group description.
- Pending estimate state is not communicated with spinner/color alone.

## 9. Do not include

- Price, store, barcode, nutrition, category/ripeness input field, history log, or delete button mixed into save area. Deletion/discard belongs to detail lifecycle action.

## 10. Requested outputs

- `edit-food_default_light_v01.png`
- `edit-food_recompute-pending_light_v01.png`
- `edit-food_save-error_light_v01.png`
