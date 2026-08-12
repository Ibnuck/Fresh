---
screen_id: my-food
screen_name: My Food
platform: iOS
framework: SwiftUI
target_os_design_language: iOS 26
reference_device: iPhone portrait 402x874pt
appearance: Light Mode
content_state: populated
status: approved-for-visual-generation
version: 2
---

# My Food

## 1. Outcome

Pengguna dapat melihat seluruh bahan menurut urgensi, mencari nama, memfilter lokasi, dan membuka detail tanpa membaca dashboard yang rumit.

## 2. Entry, exit, and primary action

- Entry: `Makananku` bottom tab atau `Lihat semua` dari Today.
- Primary: pilih satu food row.
- Secondary: search, filter storage, global Add.
- Exit: Food Detail atau Quick Add.

## 3. Three-second hierarchy

1. Title `Makananku`.
2. Search field.
3. Storage filter chips.
4. Urgency groups in order: Use Today, Use Soon, Fresh, Needs Review.
5. Bottom tabs.

## 4. Top-to-bottom layout

### Region A — Navigation

- Large title `Makananku`; trailing Settings gear.
- No item count in title.

### Region B — Search

- Native searchable placement or visible search field under title.
- Placeholder `Cari bahan` with magnifying glass; clear button native.
- Keyboard search does not hide bottom ability to dismiss naturally.

### Region C — Storage filters

- Horizontally scrollable chips with 20 pt side inset.
- Exact labels: `Semua`, `Kulkas`, `Freezer`, `Dapur`.
- `Semua` selected by default using brand-soft fill + checkmark optional.
- Filter is secondary; urgency remains section grouping.

### Region D — Grouped inventory list

- Vertical list, full-width content, 24 pt between sections.
- Section header: urgency icon/text + count; e.g. `Gunakan hari ini  1`.
- Rows use surface or minimal separators, not separate floating card for every item.
- Order/data:
  1. `Gunakan hari ini`: Bayam — `Kulkas • Dicuci, dibuka` — `Hari ini`.
  2. `Segera gunakan`: Susu segar — `Kulkas • Dibuka kemarin` — `2 hari`.
  3. `Masih fresh`: Tempe — `Kulkas • Kemasan tertutup` — `4 hari`.
  4. `Perlu ditinjau`: Alpukat — `Dekat jendela • Lokasi belum dipahami` — `Tinjau`.
- Needs Review uses slate tone and question/check icon, never red warning triangle.

### Region E — Bottom tab

- Today unselected; Add central; My Food selected.

## 5. Component inventory

| Component | SwiftUI mapping | Interaction |
|---|---|---|
| Search | `.searchable` or native search field | Filters names locally, live. |
| Filter chips | `ScrollView(.horizontal)` + buttons | Single selection. |
| Sections | `List` sections or lazy stack | Stable urgency order; hide empty section. |
| Food row | `NavigationLink` | Detail; swipe optional later, not shown in primary mockup. |

## 6. Interaction details

- Search result preserves urgency sections but hides empty groups.
- Choosing `Freezer` may show empty filter result with `Tidak ada bahan di freezer` and button `Hapus filter`.
- Tapping Alpukat opens Estimate Review or Food Detail with prominent Needs Review action; do not invent modal in image.
- Pull-to-refresh is unnecessary for local-only MVP.

## 7. States

- Global empty: illustration + `Makananku masih kosong` + `Tambahkan bahan pertama`.
- Search empty: `Tidak ada hasil untuk “…”` + clear search.
- Filter empty: location-specific text + clear filter.
- Error: `Makananmu belum dapat dimuat` + `Coba lagi`.
- Large Dynamic Type: metadata wraps; countdown moves below status, chips remain horizontally scrollable.
- Dark Mode: separator visible; colored status remains legible.

## 8. Accessibility

- Section headers are accessibility headings.
- Food rows are combined elements with name/status/countdown/storage.
- Chips announce selected state.
- Search results update announcement should not fire for every keystroke excessively.

## 9. Do not include

- Grid toggle, sorting menu, multi-select, bulk edit, prices, calories, store grouping, chart, or recipe affordance.

## 10. Requested outputs

- `my-food_populated_light_v01.png`
- `my-food_search-empty_light_v01.png`
- `my-food_dynamic-type-light_v01.png`
