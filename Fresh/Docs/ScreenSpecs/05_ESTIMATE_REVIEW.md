---
screen_id: estimate-review
screen_name: Estimate Review
platform: iOS
framework: SwiftUI
target_os_design_language: iOS 26
reference_device: iPhone portrait 402x874pt
appearance: Light Mode
content_state: estimate-available
status: approved-for-visual-generation
version: 2
---

# Estimate Review

## 1. Outcome

Pengguna memahami hasil estimasi, input/asumsi yang memengaruhinya, dan dapat menyetujui atau menyesuaikan sebelum item disimpan.

## 2. Entry, exit, and primary action

- Entry: selesai Quick Add atau field estimasi penting berubah di Edit Food.
- Primary: `Simpan bahan` untuk draft baru; `Simpan perubahan` untuk edit.
- Secondary: `Sesuaikan estimasi`, back ke input, dan `Mengapa estimasi ini?` disclosure.
- Success: dismiss sheet dan item muncul pada Today/My Food.

## 3. Three-second hierarchy

1. Nama `Bayam` dan status `Gunakan hari ini`.
2. Countdown hero `Hari ini`.
3. Disclaimer singkat bahwa ini estimasi.
4. Ringkasan input dan confidence.
5. Save CTA.

## 4. Top-to-bottom layout

### Region A — Navigation

- Inline title `Tinjau estimasi`.
- Leading back chevron; trailing `Batal` hanya bila masih di sheet creation flow.

### Region B — Estimate hero

- Centered, not a huge saturated card.
- Small ingredient thumbnail/illustration approx. 72 pt.
- Name `Bayam` in `.title2` semibold.
- Tomato-soft urgency badge `Gunakan hari ini`.
- Large value `Hari ini`; supporting `Perkiraan kualitas terbaik`.
- Disclaimer immediately below: `Ini adalah perkiraan, bukan jaminan keamanan pangan.`

### Region C — Confidence and source

- One surface card, padding 16 pt.
- Rows:
  - `Keyakinan estimasi` → `Sedang` with non-color icon.
  - `Sumber panduan` → `Aturan Fresh untuk sayuran berdaun`.
- Do not use a mysterious numerical AI percentage.
- A small label `Interpretasi Fresh` distinguishes generated/normalized values from text entered directly by the user.

### Region D — Inputs used

- Section title `Berdasarkan`.
- Compact labeled rows with check icons, preserving a clear distinction between user text and normalized interpretation:
  - `Kategori oleh Fresh` → `Sayuran berdaun`.
  - `Penyimpanan` → `Rak atas kulkas` with supporting interpretation `Kulkas`.
  - `Kondisi bahan` → `Sudah dicuci`.
  - `Status kemasan` → `Kemasan sudah dibuka`.
  - `Tanggal dibeli` → `12 Agu 2026`.
- Category is not requested during Quick Add. It is generated from the food name/context and shown here so a clearly wrong interpretation can be corrected before save.
- Disclosure button `Mengapa estimasi ini?` expands inline explanation:
  `Sayuran berdaun yang sudah dicuci biasanya perlu diprioritaskan lebih cepat. Kondisi kulkas dan bahan dapat berbeda.`

### Region E — Adjustment

- Secondary full-width outline button `Sesuaikan estimasi`.
- Supporting text `Perbaiki interpretasi atau pilih tanggal sendiri jika hasilnya tidak sesuai.`

### Region F — Bottom save dock

- Full-width primary `Simpan bahan`.
- On tap: loading indicator inside button only if save takes visible time; preserve all content.

## 5. Needs Review alternative

Jika estimasi tidak bertanggung jawab:

- Hero badge becomes slate `Perlu ditinjau`.
- Hero value `Butuh satu detail lagi`.
- Explain one exact missing or unresolved high-impact detail, for example `Fresh belum memahami lokasi penyimpanan “dekat jendela”. Perjelas lokasi agar estimasi lebih berguna.`
- Primary `Perjelas penyimpanan`; secondary `Simpan tanpa estimasi`.
- Saving without estimate is allowed and stores unknown; no invented countdown.
- Never request a separate ripeness value. Ripeness matters only when the user voluntarily includes it in `Kondisi bahan`; otherwise it remains unknown.

## 6. Save error state

- Keep sheet and draft intact.
- Inline error above CTA: `Bahan belum tersimpan. Periksa kembali lalu coba lagi.`
- Buttons: primary `Coba simpan lagi`; secondary remains adjust/back.
- Never dismiss or show success before persistence succeeds.

## 7. Component inventory

| Component | SwiftUI mapping | Behavior |
|---|---|---|
| Hero | semantic stack | Changes between estimate/needs-review. |
| Info rows | `LabeledContent`-style | Content driven height. |
| Explanation | `DisclosureGroup` | Expanded inline. |
| Adjust | `Button` | Presents date/manual estimate control. |
| Save | safe-area CTA | Throwing action; errors observable. |

## 8. Accessibility

- Hero combined value: `Bayam, gunakan hari ini, perkiraan kualitas terbaik hari ini.`
- Disclaimer is not hidden or reduced to tiny text.
- Confidence includes word, not color/icon alone.
- Error announcement occurs once and focus can move to error.

## 9. Do not include

- `Safe/unsafe`, exact AI probability, health advice, scientific chart, long citation page, forced input, or automatic save without confirmation.

## 10. Requested outputs

- Canonical: `estimate-review_available_light_v01.png`.
- Needs Review, save error, Dark Mode, disclosure, and Dynamic Type adaptations are specified in Markdown and verified during SwiftUI implementation; do not generate competing full-screen designs by default.
