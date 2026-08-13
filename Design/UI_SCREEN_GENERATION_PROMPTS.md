# Fresh UI Screen Generation Prompts

Dokumen ini berisi urutan prompt siap salin untuk satu chat khusus image generation. Kerjakan seluruh prompt di **chat yang sama**, satu per satu, sesuai urutan. Jangan mengirim semua prompt sekaligus. Tunggu setiap keluaran selesai, periksa, lalu kirim prompt berikutnya agar visual language, komponen, data, dan aset tetap konsisten.

## Cara memakai

1. Pastikan chat generator dapat membaca repository GitHub Fresh terbaru.
2. Kirim **Prompt 00** sekali untuk mengunci konteks dan sistem visual.
3. Kirim Prompt 01–08 satu per satu. Jangan membuka chat baru di tengah urutan.
4. Bila satu hasil direvisi, selesaikan revisinya sebelum lanjut ke halaman berikutnya.
5. Kirim **Prompt 09** setelah semua halaman selesai untuk audit lintas layar.
6. Jangan meminta generator mengubah source screen spec. Hasilnya adalah proposal yang nanti ditinjau dan dibawa kembali ke project Fresh.

## Keluaran wajib untuk setiap halaman

Setiap prompt halaman meminta tiga jenis keluaran:

1. **Satu mockup canonical** berupa PNG iPhone portrait untuk default/populated Light state setiap halaman; state lain tetap dijelaskan lengkap di Markdown kecuali owner meminta gambar pengecualian.
2. **Aset ilustrasi transparan** hanya bila layar benar-benar membutuhkannya. Aset harus berupa PNG RGBA tanpa background, teks, device frame, rounded-square app icon mask, atau UI di dalam gambar.
3. **Markdown implementasi UI/UX** yang cukup presisi untuk chat coding SwiftUI lain, tetapi tetap adaptif terhadap Dynamic Type dan ukuran perangkat.

Gunakan struktur paket keluaran berikut agar file mudah dipindahkan ke repository:

- mockup layar: `Design/GeneratedUI/Screens/`;
- PNG transparan: `Design/GeneratedUI/Illustrations/`;
- style lock, proposal, dan master handoff: `Design/GeneratedUI/Proposals/`.

Mockup harus beresolusi tinggi dengan rasio canvas referensi `402:874` dan tidak dibungkus device mockup. Aset transparan harus RGBA master yang cukup untuk downsampling: onboarding/empty-state minimal `2048 × 2048 px`, food thumbnail minimal `1024 × 1024 px`, dan food-detail hero minimal `2048 × 1536 px`. Pertahankan padding alpha sekitar 8–12% agar bentuk tidak terpotong. Jangan melakukan upscaling terhadap gambar kecil atau memakai checkerboard sebagai background palsu.

Di dalam setiap prompt halaman, kerjakan dengan urutan: (1) tetapkan/check ulang layout dan feature contract dari source spec, (2) generate aset transparan yang benar-benar diperlukan satu per satu, (3) gunakan aset yang sama pada canonical dan seluruh implementasi state, (4) generate satu canonical mockup, (5) tulis proposal Markdown setelah gambar final. Jangan menggambar ulang sebuah aset di dalam mockup karena bentuknya akan berubah dan continuity akan rusak.

Markdown halaman wajib memuat:

- nama/path canonical mockup, state reference yang terlanjur ada, dan seluruh aset;
- canvas referensi `402 × 874 pt`, safe area, navigation bar, tab bar, sheet, keyboard, dan scroll behavior;
- hierarchy SwiftUI dalam bentuk tree, misalnya `NavigationStack → ScrollView → VStack → Section`;
- posisi setiap region: atas/tengah/bawah, hubungan antarelemen, alignment, inset, spacing, minimum height, max width, dan frame intent dalam point;
- font menggunakan semantic Dynamic Type style dan perkiraan ukuran visual; jangan hanya menulis angka font tetap;
- token warna Light/Dark beserta hex, fungsi warna, foreground/background pairing, serta target kontras teks normal minimal `4.5:1`;
- corner radius, border, shadow, material, SF Symbols, thumbnail/illustration sizing, dan image content mode;
- reusable component mapping dan primitive SwiftUI yang realistis;
- tap target minimum `44 × 44 pt`, VoiceOver order/label/value/hint, non-color status cues, Dynamic Type, Increase Contrast, Reduce Motion, dan Dark Mode;
- perilaku populated, empty, loading, error, unavailable, keyboard, dan save failure yang relevan;
- compliance matrix terhadap source spec, assumptions, deviations, decisions needed, dan suggested spec updates;
- informasi mana yang berasal dari user dan mana yang merupakan `Interpretasi Fresh`.

Angka layout adalah intent dengan label `approx.`, bukan pixel-perfect contract. Jangan memakai absolute positioning bila stack, alignment, padding, `safeAreaInset`, `Form`, `List`, atau native toolbar dapat menghasilkan layout yang lebih adaptif.

---

## Prompt 00 — Baca repo dan kunci sistem visual

```text
Kita akan mendesain seluruh halaman aplikasi Fresh dalam CHAT YANG SAMA, satu
halaman per prompt. Jangan menghasilkan semua layar sekaligus. Pertahankan
seluruh keputusan, komponen, data contoh, dan style dari keluaran sebelumnya
ketika saya mengirim prompt berikutnya.

Baca repository GitHub Fresh terbaru terlebih dahulu. Baca lengkap dan gunakan
urutan sumber kebenaran berikut:

1. Design/README.md
2. Design/AppIcon/APP_ICON_SPEC.md
3. Design/AppIcon/APP_ICON_COMPOSER_SPEC.md
4. Design/UIConcepts/VISUAL_DIRECTION_RECONCILIATION.md
5. Fresh/Docs/VISUAL_HANDOFF_README.md
6. Fresh/Docs/APP_CONCEPT_RESEARCH.md
7. Fresh/Docs/UI_UX_DESIGN_RESEARCH.md
8. Fresh/Docs/DESIGN_SYSTEM.md
9. Fresh/Docs/VISUAL_GENERATION_GUIDE.md
10. Fresh/Docs/VisualReferences/GENERATED_UI_PROPOSAL_TEMPLATE.md
11. Semua file Fresh/Docs/ScreenSpecs/ untuk memahami flow, tetapi pada setiap
    prompt halaman nanti prioritaskan screen spec target.

Fresh adalah aplikasi native iPhone SwiftUI, bukan website dan bukan Android.
Target bahasa desain adalah iOS 26 dengan kontrol, safe area, navigation,
sheet, keyboard, Form/List, dan tab bar yang realistis dibuat secara native.

Kunci karakter visual berikut:
- 70% organic minimalism, 20% clinical clarity, 10% playful food personality;
- hangat, tenang, jujur, lapang, mudah dipindai;
- warm off-white canvas, evergreen/sage untuk brand, tomato/amber/slate hanya
  untuk status dan aksen yang memiliki teks/ikon pendamping;
- San Francisco dan Dynamic Type; tidak ada font dekoratif eksternal;
- bentuk lembut dan depth tipis yang selaras dengan ikon Sprout & Slice;
- Liquid Glass hanya pada tempat native yang wajar dan sangat terkendali,
  bukan glassmorphism berat atau tumpukan floating card;
- app icon final adalah identitas, bukan ilustrasi hero yang diulang di layar.
  Ilustrasi boleh mewarisi bentuk organik, palet, tonal variation, highlight,
  dan kedalamannya, tetapi jangan menyalin komposisi daun-jam-tomat lengkap.

Inspeksi secara visual `Design/AppIcon/AppIcon_Foreground_Official.png` dan
`Design/UIConcepts/fresh_ui_visual_direction.png`, bukan hanya nama/deskripsi
filenya. Gunakan keduanya untuk menyelaraskan bentuk dan rendering. Orange
`#FF8D28` adalah background Default app icon yang dipilih demi kontras; warna
itu boleh menjadi aksen hangat terbatas, tetapi bukan pengganti canvas warm
off-white atau brand evergreen pada seluruh UI.

Aturan produk yang tidak boleh berubah:
- navigasi utama hanya Hari ini, action global Tambah, dan Makananku;
- Settings berada di toolbar, bukan tab keempat;
- search hanya ada di Makananku; tidak ada global search;
- foto bahan hanya dekoratif/pengenal visual, bukan input analisis wajib;
- user tidak menginput kategori; Fresh menghasilkan kategori dan menampilkannya
  sebagai Interpretasi Fresh untuk ditinjau;
- Lokasi penyimpanan, Kondisi bahan, dan Status kemasan adalah text field bebas;
- tingkat kematangan bukan field terpisah; bila user menyebutkannya, informasi
  itu menjadi bagian Kondisi bahan. Jika tidak disebut, nilainya unknown dan
  tidak boleh ditebak dari toko atau kebiasaan produk;
- tanggal beli/tanggal acuan tetap dipilih user;
- tidak ada recipe, shopping list, nutrition, barcode/OCR, cloud sync,
  household sharing, analytics, account, paywall, atau fitur sosial;
- freshness adalah estimasi kualitas/prioritas, bukan jaminan makanan aman atau
  tidak aman. Jangan gunakan copy safe to eat atau unsafe to eat;
- status selalu memakai teks dan/atau ikon, tidak boleh bergantung pada warna.

Gunakan continuity dataset yang tertulis di VISUAL_GENERATION_GUIDE.md secara
konsisten: Bayam, Susu segar, Tempe, dan Alpukat beserta metadata/statusnya.

Sekarang JANGAN membuat mockup halaman. Buat terlebih dahulu satu dokumen
`Design/GeneratedUI/Proposals/FRESH_VISUAL_STYLE_LOCK.md` berisi:
1. ringkasan prinsip visual;
2. token warna Light/Dark dengan hex dan pasangan kontras;
3. typography roles berbasis Dynamic Type;
4. spacing, radius, border, shadow, dan material rules;
5. reusable component inventory;
6. aturan ilustrasi PNG transparan dan thumbnail bahan;
7. aturan navigation/tab/sheet/form;
8. continuity dataset dan asset reuse manifest awal;
9. daftar larangan produk/visual;
10. checklist konsistensi yang akan dipakai pada semua prompt berikutnya.

Jangan membuat keputusan baru terkait fitur atau navigasi. Jika ada konflik,
screen spec target mengalahkan dokumen visual lain. Tunjukkan ringkasan singkat
apa yang kamu pahami dan isi style lock tersebut, lalu tunggu prompt berikutnya.
```

---

## Prompt 01 — Onboarding dan tiga ilustrasi transparan

```text
Lanjutkan di chat dan visual system yang sama. Jangan mereset style atau
menginterpretasikan ulang produk. Baca ulang
`Design/GeneratedUI/Proposals/FRESH_VISUAL_STYLE_LOCK.md`, lalu
baca lengkap `Fresh/Docs/ScreenSpecs/01_ONBOARDING.md` beserta dokumen global
yang diwajibkan oleh `Fresh/Docs/VISUAL_GENERATION_GUIDE.md`.

Buat desain final proposal Onboarding tiga langkah sesuai exact Indonesian copy
di screen spec. Ketiga layar harus tampak sebagai satu sequence yang sama:
layout, ukuran ilustrasi, message block, progress indicator, CTA dock, posisi
Lewati/back, dan transition intent harus konsisten.

Hasilkan mockup berikut:
- `onboarding_step1_light_v01.png`
- `onboarding_step2_light_v01.png`
- `onboarding_step3_light_v01.png`

Buat tiga ilustrasi terpisah yang benar-benar transparan dan dapat langsung
dipakai sebagai SwiftUI Image asset:
- `onboarding_01_use_what_you_have_transparent.png`
- `onboarding_02_calm_reminder_transparent.png`
- `onboarding_03_start_one_item_transparent.png`

Ilustrasi master minimal `2048 × 2048 px` dan harus mengikuti konsep masing-masing step di screen spec, memiliki
alpha bersih, ruang transparan secukupnya, tidak berisi teks/UI/button/device
frame/background, dan selaras dengan karakter organik ikon tanpa menyalin app
icon. Jangan membuatnya seperti foto komersial atau emoji besar.

Selain gambar, buat `onboarding_GENERATED_UI_PROPOSAL.md` memakai template repo.
Tambahkan tabel spesifikasi masing-masing step, hierarchy SwiftUI, safe-area dan
CTA behavior, exact font roles, hex warna, approx. frames/insets/spacing,
illustration placement/content mode, progress dimensions, keyboard/scroll yang
relevan, VoiceOver order, Dynamic Type, Dark Mode adaptation, Reduce Motion,
asset manifest, compliance matrix, assumptions, dan deviations.

Periksa khusus: ilustrasi maksimal sekitar 35% tinggi layar, body maksimal tiga
baris pada ukuran default, CTA tidak overlap pada Dynamic Type, tidak ada prompt
notifikasi/login/paywall/statistik/recipe. Setelah selesai, ringkas keputusan
visual yang harus dipertahankan oleh halaman berikutnya dan tunggu prompt saya.
```

---

## Prompt 02 — Today canonical

```text
Lanjutkan dari hasil Onboarding dalam chat yang sama. Pertahankan style lock,
komponen yang sudah disepakati, dan bahasa ilustrasinya. Baca lengkap
`Fresh/Docs/ScreenSpecs/02_TODAY.md` serta screen tujuan yang terkait:
`03_MY_FOOD.md`, `04_QUICK_ADD.md`, `06_FOOD_DETAIL.md`, dan `08_SETTINGS.md`.

Buat satu canonical mockup `today_populated_light_v01.png`. Empty, Dark Mode,
loading/error/all-caught-up, dan Dynamic Type dijelaskan di proposal Markdown;
jangan membuat bitmap tambahan kecuali owner meminta pengecualian.

Ikuti hierarchy tiga detik dan exact copy/data dari spec. Gunakan native large
navigation title, Settings gear, prominent Bayam priority card, Susu segar row,
satu suggestion strip, dan bottom tab dengan Hari ini / Tambah / Makananku.
Tidak ada search pada halaman ini.

Buat hanya aset transparan yang benar-benar diperlukan:
- `today_empty_kitchen_container_transparent.png` untuk empty state;
- `food_thumbnail_bayam_transparent.png` dan
  `food_thumbnail_susu_transparent.png` bila thumbnail reusable belum dibuat.

Jangan menggambar ulang thumbnail yang sudah ada; masukkan ke asset reuse
manifest. Aset empty-state minimal `2048 × 2048 px`, thumbnail minimal
`1024 × 1024 px`, dan semuanya tanpa teks, badge, card, background, atau device frame.

Buat `today_GENERATED_UI_PROPOSAL.md` memakai template. Dokumentasikan tree
SwiftUI, large-title collapse/scroll, exact region positions, card/row geometry,
tab bar dan central Add behavior, semantic colors dan contrast pairing, Light
ke Dark mapping, SF Symbols, approx. sizes/spacing, hit targets, full-row tap,
VoiceOver combined values, empty/loading/error/all-caught-up states, Dynamic
Type adaptations, asset reuse, compliance, dan deviasi.

Pastikan tidak ada dashboard analytics, waste score, streak, recipe, shopping
list, chat assistant, atau lebih dari dua urgency sections pada viewport awal.
Setelah selesai, ringkas reusable component yang dikunci untuk My Food dan
tunggu prompt berikutnya.
```

---

## Prompt 03 — My Food dan search satu-satunya

```text
Lanjutkan di chat yang sama dan gunakan reusable FoodRow, urgency badge, tab bar,
thumbnail, colors, typography, dan spacing dari Today. Baca lengkap
`Fresh/Docs/ScreenSpecs/03_MY_FOOD.md` dan reread `02_TODAY.md` serta
`06_FOOD_DETAIL.md` untuk continuity.

Buat satu canonical mockup `my-food_populated_light_v01.png`. Search/filter/global
empty, Dark Mode, dan Dynamic Type dijelaskan di proposal Markdown; jangan membuat
bitmap tambahan kecuali owner meminta pengecualian.

Makananku adalah SATU-SATUNYA halaman MVP yang memiliki search. Gunakan native
search field `Cari bahan`, storage filter chips Semua/Kulkas/Freezer/Dapur, dan
urgency sections stabil berisi Bayam, Susu segar, Tempe, dan Alpukat sesuai
continuity dataset. Needs Review harus slate dengan teks/ikon, bukan red warning.

Gunakan ulang thumbnail Bayam dan Susu. Bila belum ada, buat aset transparan:
- `food_thumbnail_tempe_transparent.png`
- `food_thumbnail_alpukat_transparent.png`

Jangan membuat illustration baru bila existing reusable asset sudah cukup.

Buat `my-food_GENERATED_UI_PROPOSAL.md` memakai template, mencakup populated,
search-empty, dan Dynamic Type state; search focus dan keyboard behavior, clear
button, horizontal chip scrolling, selected state,
grouped list structure, stable urgency order, row dimensions, section spacing,
bottom tabs, search/filter/global empty/error states, Dynamic Type row reflow,
Dark mapping, accessibility combined labels, exact tokens/hex/contrast,
SwiftUI mapping, asset manifest, compliance, assumptions, dan deviations.

Jangan membuat global search, category tabs, pull-to-refresh, swipe-only action,
dashboard, atau kategori sebagai input user. Ringkas continuity decisions dan
tunggu prompt selanjutnya.
```

---

## Prompt 04 — Quick Add satu form

```text
Lanjutkan style dan komponen dari halaman sebelumnya. Baca lengkap versi terbaru
`Fresh/Docs/ScreenSpecs/04_QUICK_ADD.md`, lalu reread `05_ESTIMATE_REVIEW.md` dan
`07_EDIT_FOOD.md` agar input, interpretation, dan review flow tidak bertentangan.

Buat satu canonical mockup `quick-add_form_light_v01.png`. Ini adalah satu
native large-detent sheet/NavigationStack dengan form scrollable, bukan wizard
bertahap. Header hanya `Batal` dan `Tambah bahan`, tanpa progress counter.
Bottom CTA `Tinjau estimasi` memakai safe-area inset dan tidak tertutup keyboard.
Canonical boleh menunjukkan keyboard dismissed agar seluruh input terlihat;
focus/keyboard behavior harus tetap dijelaskan di proposal Markdown.

Aturan input wajib terlihat jelas:
- Nama bahan: text field wajib;
- foto: opsional dan hanya hiasan/pengenal visual, bukan sumber analisis wajib;
- Lokasi penyimpanan: free-text text field, bukan picker/chips;
- Kondisi bahan: free-text text field; tingkat kematangan hanya boleh ditulis
  alami di sini dan tidak menjadi field terpisah;
- Status kemasan: free-text text field, bukan pilihan tetap;
- kategori tidak pernah ditanyakan kepada user;
- tanggal acuan memakai `Tanggal pada kemasan`, `Tanggal dibeli`, atau
  `Tidak ada tanggal` dan kontrol tanggal native bila relevan;
- detail yang tidak diberikan tetap unknown dan tidak boleh ditebak.

Tidak perlu ilustrasi hero baru untuk Quick Add. Gunakan photo placeholder/fallback
yang ringan atau reuse thumbnail bahan hanya bila sesuai spec. Jangan membuat
aset dekoratif yang mengurangi fokus pada input.

Buat `quick-add_GENERATED_UI_PROPOSAL.md` yang menjelaskan satu form lengkap:
navigation/sheet, scroll/focus state, keyboard type, setiap field label/hint/error,
stack tree, approx. frames/insets/spacing, CTA enabled/disabled, date-choice
interaction, draft preservation, discard confirmation, VoiceOver, Dynamic Type,
Dark Mode, local-intelligence unavailable fallback, exact colors/contrast,
SwiftUI primitive mapping, compliance, dan deviations.

Jangan menambah category picker, ripeness control, storage presets, package
chips, barcode/OCR, AI chat, atau price/store. Semua core field memang berada
dalam satu form, tetapi `Detail lainnya` tetap collapsed. Setelah selesai, kunci
pola form yang akan digunakan Edit Food dan tunggu prompt.
```

---

## Prompt 05 — Estimate Review dan transparansi estimasi

```text
Lanjutkan flow Quick Add di chat yang sama. Baca lengkap versi terbaru
`Fresh/Docs/ScreenSpecs/05_ESTIMATE_REVIEW.md` dan reread `04_QUICK_ADD.md` serta
`07_EDIT_FOOD.md`. Gunakan raw input yang sama dan tunjukkan pemisahan jelas
antara ucapan user dan `Interpretasi Fresh`.

Buat satu canonical mockup `estimate-review_available_light_v01.png`. Needs
Review, save error, disclosure expansion, Dark Mode, dan Dynamic Type dijelaskan
di proposal Markdown; jangan membuat bitmap tambahan kecuali owner meminta
pengecualian.

Gunakan kembali `food_thumbnail_bayam_transparent.png`; jangan menghasilkan Bayam
baru dengan style berbeda. Hero harus informatif dan tenang, bukan kartu besar
saturated. Exact disclaimer harus terbaca dekat estimasi. Category tampil sebagai
`Kategori oleh Fresh`, bukan field yang sebelumnya diisi user.

Needs Review tidak boleh mengarang countdown. Gunakan contoh lokasi Alpukat yang
belum dipahami sesuai spec, satu permintaan detail yang spesifik, primary action
untuk memperjelas, dan opsi menyimpan tanpa estimasi. Save error harus menjaga
draft dan sheet tetap terbuka.

Buat `estimate-review_GENERATED_UI_PROPOSAL.md` memakai template. Sertakan tree
SwiftUI, navigation, hero geometry, confidence/source card, labeled rows,
DisclosureGroup collapsed/expanded behavior, adjustment button, save dock,
loading/error focus behavior, exact tokens/hex/contrast, typography/spacing,
status non-color cues, VoiceOver combined estimate, Dynamic Type, Dark mapping,
data provenance labels, asset reuse, compliance, assumptions, dan deviations.

Jangan memakai safe/unsafe verdict, AI percentage, scientific chart, health
advice, hidden disclaimer, forced missing input, atau autosave. Ringkas pola
transparency yang harus dipakai Food Detail lalu tunggu prompt berikutnya.
```

---

## Prompt 06 — Food Detail dan lifecycle actions

```text
Lanjutkan dari Today dan Estimate Review. Baca lengkap versi terbaru
`Fresh/Docs/ScreenSpecs/06_FOOD_DETAIL.md`, lalu reread `02_TODAY.md`,
`03_MY_FOOD.md`, `05_ESTIMATE_REVIEW.md`, dan `07_EDIT_FOOD.md`.

Buat satu canonical mockup `food-detail_use-today_light_v01.png`. Needs Review,
Dark Mode, persistence failure, dan unavailable state dijelaskan di proposal
Markdown; jangan membuat bitmap tambahan kecuali owner meminta pengecualian.

Gunakan data Bayam yang sama. Buat satu aset hero transparan hanya bila thumbnail
yang sudah ada tidak memiliki resolusi/komposisi memadai:
- `food_detail_bayam_hero_transparent.png`

Jika dibuat, hero harus berupa bahan Bayam alami/ilustratif yang selaras dengan
asset family, tanpa background/card/UI/text. Dokumentasikan apakah thumbnail
diturunkan dari hero atau tetap aset terpisah; jangan membuat gaya Bayam kedua
yang tidak konsisten. Master hero minimal `2048 × 1536 px` dengan alpha bersih.

Ikuti exact hero, urgency/countdown, disclaimer, timeline tiga titik, primary
`Sudah digunakan`, secondary Bekukan/Pindahkan, destructive Buang yang terpisah,
Why card, dan storage tip. Timeline menjelaskan estimasi kualitas, bukan batas
kesehatan. Foto/ilustrasi bersifat visual dan bukan bukti keamanan.

Buat `food-detail_GENERATED_UI_PROPOSAL.md` dengan layout tree, scroll/nav title
behavior, hero size/content mode, timeline structure, action layout dan large
text stacking, sheets/dialogs untuk lifecycle actions, persistence failure dan
rollback visibility, why disclosure, storage tip, exact typography/tokens/hex/
contrast, Light/Dark mapping, VoiceOver chronology, non-color urgency cues,
Dynamic Type, Reduce Motion, unavailable deep-link state, asset reuse manifest,
compliance, assumptions, dan deviations.

Jangan menambah recipe carousel, nutrition, store map, share, AI chat, safety
verdict, atau giant floating action menu. Ringkas reusable detail/form decisions
dan tunggu prompt berikutnya.
```

---

## Prompt 07 — Edit Food

```text
Lanjutkan dalam visual system yang sama. Baca lengkap versi terbaru
`Fresh/Docs/ScreenSpecs/07_EDIT_FOOD.md`, lalu reread `04_QUICK_ADD.md`,
`05_ESTIMATE_REVIEW.md`, dan `06_FOOD_DETAIL.md`.

Buat satu canonical mockup `edit-food_default_light_v01.png`. Recompute pending,
save error, Dark Mode, dan Dynamic Type dijelaskan di proposal Markdown; jangan
membuat bitmap tambahan kecuali owner meminta pengecualian.

Gunakan native sheet dengan NavigationStack dan pola field Quick Add yang sama.
Kelompokkan field yang memengaruhi estimasi lebih dulu. Lokasi, kondisi, dan
status kemasan tetap free-text. Jangan membuat category/ripeness input. Generated
category hanya boleh tampil sebagai read-only `Interpretasi Fresh` dan ditinjau
di Estimate Review saat recompute.

Reuse thumbnail/hero Bayam yang sudah ada; tidak perlu aset ilustrasi baru.

Buat `edit-food_GENERATED_UI_PROPOSAL.md` dengan tree SwiftUI/Form, navigation
dan unsaved-changes confirmation, visible-label field layout, keyboard/focus,
estimate-affecting vs other-details groups, photo decorative semantics, current/
pending estimate preview, CTA routing (`Tinjau perubahan` vs `Simpan`), disabled
and error states, draft preservation, exact approx. dimensions/spacing/font,
tokens/hex/contrast, Dynamic Type vertical reflow, Dark mapping, VoiceOver,
asset reuse, compliance, assumptions, dan deviations.

Jangan menambah price, store, barcode, nutrition, history log, category/ripeness
field, autosave, atau delete action di save area. Setelah selesai, ringkas pola
form final dan tunggu prompt berikutnya.
```

---

## Prompt 08 — Settings

```text
Lanjutkan style lock dan pola native yang sama. Baca lengkap versi terbaru
`Fresh/Docs/ScreenSpecs/08_SETTINGS.md` serta bagian privacy/intelligence/safety
dari dokumen produk dan design system.

Buat satu canonical mockup `settings_default_light_v01.png`. Notification denied,
Dark Mode, permission feedback, dan unavailable intelligence dijelaskan di
proposal Markdown; jangan membuat bitmap tambahan kecuali owner meminta
pengecualian.

Gunakan native pushed page dan grouped Form. Ikuti urutan Pengingat, Tampilan
tanggal, Privacy dan intelligence, Tentang estimasi, lalu onboarding/version.
Pada primary visual, omit `Hapus semua data Fresh…` karena masih optional/deferred
menurut screen spec. `Interpretasi pintar di perangkat` adalah availability
status, bukan toggle palsu. Notification denied harus menampilkan pesan dan
`Buka Pengaturan iPhone`, bukan toggle on yang seolah berhasil.

Tidak perlu ilustrasi PNG khusus Settings. Gunakan SF Symbols yang aman dan
native; jangan memakai Apple Intelligence logo.

Buat `settings_GENERATED_UI_PROPOSAL.md` dengan hierarchy Form/Section/row,
navigation behavior, toggle/time picker states, permission flow, error feedback,
footer wrapping, exact typography/tokens/hex/contrast, row minimum height,
Light/Dark grouped surfaces, Dynamic Type, VoiceOver labels/values, system
settings destination hint, intelligence unavailable state, compliance,
assumptions, dan deviations.

Jangan menambah account, subscription, cloud sync, household sharing, theme
picker, developer menu, recipe preferences, nutrition goals, atau analytics.
Setelah selesai, ringkas komponen Settings dan tunggu prompt audit akhir.
```

---

## Prompt 09 — Audit seluruh desain dan paket handoff

```text
Semua halaman Fresh sudah dibuat dalam chat ini. Jangan membuat redesign baru.
Audit seluruh hasil terhadap repository terbaru,
`Design/GeneratedUI/Proposals/FRESH_VISUAL_STYLE_LOCK.md`,
semua source screen specs, dan semua proposal Markdown yang sudah kamu hasilkan.

Periksa lintas layar:
1. app ini selalu tampak native iOS SwiftUI pada canvas 402x874 pt;
2. navigation hanya Hari ini / Tambah / Makananku dan Settings di toolbar;
3. search hanya ada di Makananku;
4. Bayam, Susu segar, Tempe, Alpukat, status, tanggal, dan metadata konsisten;
5. FoodRow, badges, CTA, fields, tabs, nav, sheets, cards, dan spacing konsisten;
6. typography berbasis Dynamic Type dan warna Light/Dark memiliki kontras yang
   dapat dipertanggungjawabkan;
7. status selalu memiliki teks/ikon selain warna;
8. disclaimer freshness konsisten dan tidak pernah menjadi safety verdict;
9. kategori selalu generated; lokasi/kondisi/kemasan selalu free-text; ripeness
   tidak pernah menjadi field atau tebakan; unknown tetap unknown;
10. foto/ilustrasi hanya visual dan tidak dinyatakan sebagai analisis wajib;
11. semua transparent PNG benar-benar RGBA, tanpa background/UI/text/device;
12. aset yang sama digunakan ulang dan tidak berubah style antarhalaman;
13. ikon app tidak diulang sebagai hero generik;
14. tidak ada fitur di luar scope;
15. semua Markdown memiliki stack tree, approx. layout specs, font roles, hex,
    contrast, states, accessibility, SwiftUI mapping, compliance, dan deviasi.

Buat `Design/GeneratedUI/Proposals/FRESH_GENERATED_UI_MASTER_HANDOFF.md` yang berisi:
- daftar semua mockup dan transparent assets beserta path/nama;
- final token table dan reusable component table;
- cross-screen navigation map;
- asset reuse map;
- exact-copy consistency report;
- accessibility and contrast audit;
- per-screen compliance summary;
- daftar deviations dan decisions needed yang masih memerlukan persetujuan;
- rekomendasi urutan implementasi SwiftUI per roadmap goal;
- instruksi jelas untuk chat coding agar membaca proposal tanpa menganggapnya
  otomatis mengubah source spec.

Jika menemukan inkonsistensi kecil, koreksi proposal/asset yang bersangkutan dan
catat perubahannya. Jika inkonsistensi mengubah fitur, navigasi, data, safety,
atau primary action, jangan putuskan sendiri—masukkan ke `Decisions needed`.

Terakhir, berikan satu paket daftar file yang harus saya unduh/kirim kembali ke
project Fresh. Jangan hanya memberi ringkasan chat; semua informasi implementasi
harus ada di Markdown yang berdiri sendiri.
```

## Catatan setelah generator selesai

Hasil generator belum otomatis menjadi source of truth. Bawa seluruh PNG dan Markdown kembali ke project Fresh. Review deviasi dan `Decisions needed`, lalu hanya keputusan yang disetujui yang boleh dimasukkan ke screen spec atau design system sebelum coding dimulai.
