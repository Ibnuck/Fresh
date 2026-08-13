---
screen_id: today
screen_name: Today
platform: iOS
framework: SwiftUI
target_os_design_language: iOS 26
reference_device: iPhone portrait 402x874pt
appearance: Light Mode
content_state: populated-and-empty
status: approved-for-visual-generation
version: 1
---

# Today

## 1. Outcome

Pengguna dalam beberapa detik mengetahui bahan yang paling perlu diperhatikan dan dapat membuka detail atau menambah bahan.

## 2. Entry, exit, and primary action

- Entry: default tab setelah onboarding.
- Primary action populated: tap bahan pada `Gunakan hari ini`.
- Primary action empty: `Tambahkan bahan`.
- Secondary: tap `Lihat semua`, global Add, atau Settings.
- Destination: Food Detail, My Food, Quick Add sheet, Settings.

## 3. Three-second hierarchy

1. Title `Hari ini` dan greeting singkat berbasis waktu yang tidak personal berlebihan.
2. `Gunakan hari ini` dengan Bayam dan label `Hari ini`.
3. `Segera gunakan` dengan Susu segar.
4. Saran satu kalimat yang dapat ditindak.
5. Bottom navigation.

## 4. Populated top-to-bottom layout

### Region A — Navigation bar

- Large navigation title `Hari ini` di leading.
- Trailing gear button dengan label accessibility `Buka pengaturan`.
- Canvas background, tanpa card header.

### Region B — Context line

- Tepat di bawah title, inset 20 pt.
- Copy `Yang paling berguna untuk diperhatikan sekarang.` dalam `.subheadline` secondary.
- Tidak ada angka waste, streak, score, atau chart.

### Region C — Use Today section

- Section header HStack: `Gunakan hari ini` leading; `Lihat semua` trailing.
- Satu prominent food card full content width; tomato-soft tint sangat ringan.
- Card layout: thumbnail Bayam 64 pt leading; center nama `Bayam`, metadata `Kulkas • Dicuci, dibuka`; badge `Gunakan hari ini`; trailing countdown `Hari ini` dan chevron.
- Card minimum height approx. 104 pt; entire card tappable.

### Region D — Use Soon section

- 24 pt setelah prioritas pertama.
- Header `Segera gunakan`.
- Food row Susu segar: `Kulkas • Dibuka kemarin`, badge `Segera gunakan`, trailing `2 hari`.
- Visual emphasis lebih rendah dari Use Today; amber tone lembut.

### Region E — Suggestion strip

- Surface sage lembut, icon `lightbulb` atau `leaf`, bukan chat bubble.
- Title `Saran kecil`.
- Body `Letakkan bayam di bagian depan kulkas agar mudah terlihat saat memasak.`
- Tidak ada tombol recipe.

### Region F — Bottom tab bar

- Native anchored bottom: Today selected, central Add, My Food unselected.
- Labels exact: `Hari ini`, `Tambah`, `Makananku`.
- Central Add uses plus icon and brand accent; 44 pt+ target.

## 5. Empty state layout

- Navigation dan bottom tab sama.
- Center content vertically above tab bar, but slightly above optical center.
- Illustration: wadah/kulkas sederhana dengan satu leaf; max width 220 pt.
- Title `Belum ada bahan untuk dipantau`.
- Body `Tambahkan bahan dari dapurmu. Fresh akan membantu mengurutkan mana yang perlu dipakai lebih dulu.`
- Primary full-width/contained button `Tambahkan bahan`.
- Secondary text `Kamu bisa mulai hanya dengan nama dan lokasi penyimpanan.`

## 6. Component inventory

| Component | SwiftUI mapping | Behavior |
|---|---|---|
| Screen | `NavigationStack` + `ScrollView`/`List` | Content scroll; large title collapses natively. |
| Priority card | custom `Button`/`NavigationLink` | Opens Bayam detail. |
| Food row | reusable `FoodRow` | Opens item detail; accessible combined element. |
| Suggestion | semantic surface | Static guidance for MVP. |
| Tabs | `TabView` plus Add presentation | Maintains selected tab. |

## 7. Data and exact copy

- Bayam: `Kulkas • Dicuci, dibuka`, `Gunakan hari ini`, `Hari ini`.
- Susu segar: `Kulkas • Dibuka kemarin`, `Segera gunakan`, `2 hari`.
- Do not show Tempe/Alpukat on populated Today default; they live in My Food.

## 8. States

- Loading: local SwiftData load should be near-instant; use redacted rows only if truly asynchronous later, not a spinner by default.
- Persistence/read error: inline surface `Makananmu belum dapat dimuat` + `Coba lagi`; keep navigation available.
- All caught up: replace sections with calm message `Tidak ada yang mendesak hari ini` and show next item optionally.
- Large Dynamic Type: food row becomes vertical; countdown stays near item, not clipped.
- Dark Mode: urgency surfaces remain subtle, avoid saturated blocks.

## 9. Accessibility

- Bayam combined value: `Bayam, gunakan hari ini, hari ini, disimpan di kulkas, dicuci dan dibuka.`
- Susu: `Susu segar, segera gunakan, perkiraan dua hari, disimpan di kulkas, dibuka kemarin.`
- `Lihat semua` hint: `Membuka semua bahan di Makananku`.

## 10. Do not include

- Analytics, total waste saved, recipe cards, shopping list, calories, achievements, chat assistant, or more than two urgency sections in the first viewport.

## 11. Requested outputs

- Canonical: `today_populated_light_v01.png` (the accepted generated implementation anchor may use a later reviewed version suffix).
- Empty, Dark Mode, loading/error/all-caught-up, and Dynamic Type are Markdown implementation states; existing reviewed alternate-state images are supplementary only.
