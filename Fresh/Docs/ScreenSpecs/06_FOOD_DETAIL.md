---
screen_id: food-detail
screen_name: Food Detail
platform: iOS
framework: SwiftUI
target_os_design_language: iOS 26
reference_device: iPhone portrait 402x874pt
appearance: Light Mode
content_state: use-today
status: approved-for-visual-generation
version: 2
---

# Food Detail

## 1. Outcome

Pengguna dapat memahami status dan alasan estimasi Bayam, lalu mencatat apa yang terjadi pada bahan melalui lifecycle actions yang jelas.

## 2. Entry, exit, and primary action

- Entry: tap Bayam from Today/My Food.
- Primary: `Sudah digunakan`.
- Secondary: `Bekukan`, `Pindahkan`, `Buang`, `Edit`.
- Back returns to originating tab; updates appear immediately after successful persistence.

## 3. Three-second hierarchy

1. Bayam visual/name.
2. `Gunakan hari ini` + `Hari ini` countdown.
3. Disclaimer and freshness timeline.
4. Primary lifecycle action.
5. Explanation/storage details.

## 4. Top-to-bottom layout

### Region A — Navigation

- Inline title may be visually hidden until scroll; leading back.
- Trailing `Edit` text button, not ellipsis-only.

### Region B — Hero

- Food photo/illustration full content width with approx. 180–220 pt height and 16 pt radius, inset 20 pt; natural Bayam.
- Below: `Bayam`, metadata `Kulkas • Dicuci, dibuka`.
- Urgency badge `Gunakan hari ini` and hero countdown `Hari ini`.
- Subtext `Perkiraan kualitas terbaik`.
- Disclaimer `Periksa kondisi bahan sebelum digunakan. Estimasi bukan jaminan keamanan.`

### Region C — Freshness timeline

- Section `Perjalanan kesegaran`.
- Horizontal/vertical accessible timeline with three named points, not color only:
  - `Ditambahkan` — `12 Agu`.
  - `Gunakan hari ini` — `Hari ini`, current highlighted.
  - `Lewat perkiraan` — `Setelah hari ini`.
- Timeline is explanatory, not a precise health boundary.

### Region D — Primary actions

- Full-width brand button `Sudah digunakan` with checkmark.
- Two equal secondary buttons below only if labels fit: `Bekukan` (snowflake), `Pindahkan` (arrow). At large text, stack vertically.
- `Buang` is destructive text/button farther below, not beside primary CTA.

### Region E — Why card

- Disclosure/card title `Mengapa estimasi ini?`.
- Summary rows: storage, condition, reference date, source, confidence.
- Explanation exact: `Sayuran berdaun yang sudah dicuci biasanya perlu diprioritaskan lebih cepat. Kondisi bahan dan suhu kulkas dapat berbeda.`

### Region F — Storage tip

- Sage-soft information surface.
- Title `Tips penyimpanan`.
- Copy `Jaga tetap dingin dan keringkan kelembapan berlebih bila memungkinkan.`
- No link to recipe or shopping.

## 5. Lifecycle interactions

- `Sudah digunakan`: confirmation optional only if reversible strategy absent; on success item leaves active inventory with subtle feedback.
- `Bekukan`: opens small confirmation sheet asking date and optional note; recalculates using frozen state.
- `Pindahkan`: sheet with a visible-label text field `Lokasi penyimpanan`, for example `rak bawah kulkas`; recalculates after the new text is interpreted, reviewed when ambiguous, and successfully saved.
- `Buang`: destructive confirmation `Buang Bayam dari daftar?`; copy should not shame user.
- Persistence failure: action sheet/detail stays, previous state restored or clearly marked; show `Perubahan belum tersimpan. Coba lagi.`

## 6. Component inventory

| Component | SwiftUI mapping | Behavior |
|---|---|---|
| Hero image | `Image`/`AsyncImage` future | Decorative and semantic name handled once. |
| Timeline | custom accessible stack | Current step announced. |
| Actions | `Button`/confirmation dialog/sheet | Throwing lifecycle service. |
| Explanation | `DisclosureGroup` or card | Transparent inputs/source. |

## 7. States

- Needs Review item: replace countdown with `Tinjau estimasi`; primary action opens missing field.
- Used/discarded stale deep link: show unavailable explanation and back action.
- Large Dynamic Type: timeline vertical; action grid becomes stack.
- Dark Mode: image still natural; tomato/sage surfaces restrained.

## 8. Accessibility

- Do not read `Bayam` three times across image/title/card; decorative image hidden.
- Countdown announces estimate context.
- Destructive action has explicit name and confirmation.
- Timeline elements have chronological order and current value.

## 9. Do not include

- Safety verdict, recipe carousel, nutrition, price, store map, social share, AI chatbot, or giant floating action menu.

## 10. Requested outputs

- `food-detail_use-today_light_v01.png`
- `food-detail_use-today_dark_v01.png`
- `food-detail_needs-review_light_v01.png`
