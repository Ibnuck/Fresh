# Fresh Visual Handoff — Start Here

Dokumen ini adalah pintu masuk untuk chat/AI lain yang bertugas membuat gambar UI dan menulis Markdown UI/UX. Anda tidak perlu membaca percakapan asal proyek.

## Tentang produk

Fresh adalah aplikasi iPhone native SwiftUI untuk membantu pengguna rumahan mengingat bahan makanan, memahami mana yang perlu dipakai lebih dulu, dan mengurangi bahan terbuang. Fresh bukan aplikasi diagnosis keamanan pangan, penghitung nutrisi, recipe app, atau dashboard statistik.

## Tugas chat visual

1. Baca dokumen dalam urutan berikut:
   - `../../Design/README.md` untuk status identitas dan artefak visual;
   - `../../Design/UIConcepts/VISUAL_DIRECTION_RECONCILIATION.md` untuk batas penggunaan katalog konsep;
   - `APP_CONCEPT_RESEARCH.md` untuk konteks produk;
   - `UI_UX_DESIGN_RESEARCH.md` untuk dasar keputusan visual;
   - `DESIGN_SYSTEM.md` untuk aturan global;
   - `VISUAL_GENERATION_GUIDE.md` untuk cara menghasilkan gambar dan Markdown;
   - satu file target di `ScreenSpecs/`.
2. Buat satu atau beberapa mockup iPhone portrait sesuai state yang diminta.
3. Jangan menambah fitur, copy, atau navigasi yang tidak tertulis.
4. Setelah membuat gambar, tulis proposal Markdown memakai format `VisualReferences/GENERATED_UI_PROPOSAL_TEMPLATE.md`.
5. Tandai semua penyimpangan dari spec sebagai usulan, bukan keputusan.

## Sumber kebenaran dan prioritas

Jika dokumen berbeda, gunakan urutan prioritas berikut:

1. Screen spec target.
2. `DESIGN_SYSTEM.md`.
3. `VISUAL_GENERATION_GUIDE.md`.
4. `../../Design/UIConcepts/VISUAL_DIRECTION_RECONCILIATION.md`.
5. Gambar konsep di `../../Design/`.
6. Research documents.
7. Interpretasi visual Anda sendiri.

## Status app icon

Sprout & Slice adalah konsep yang dipilih, tetapi artwork runtime final belum selesai. Untuk pekerjaan ikon, baca `../../Design/AppIcon/APP_ICON_SPEC.md`. Jangan memakai atau menciptakan ulang tiga layer lama; output berikutnya harus satu foreground transparan yang meniru gambar konsep sedekat mungkin. Background akan diatur oleh pemilik di Apple Icon Composer.

## Batas penting

- Platform hanya iOS portrait; jangan membuat website atau Android.
- Gunakan pola kontrol native iOS dan tampilan yang realistis untuk SwiftUI.
- Jangan memakai kalimat `safe to eat`, `unsafe to eat`, atau klaim keamanan absolut.
- Countdown adalah estimasi kualitas/kesegaran, bukan jaminan keamanan.
- Status tidak boleh bergantung pada warna saja: selalu gunakan teks dan/atau ikon.
- Pertahankan contoh data lintas layar agar alur terasa seperti aplikasi yang sama.

## Daftar layar

| ID | File | Fungsi |
|---|---|---|
| `onboarding` | `ScreenSpecs/01_ONBOARDING.md` | Memperkenalkan manfaat dan menuju item pertama. |
| `today` | `ScreenSpecs/02_TODAY.md` | Menunjukkan tindakan paling berguna hari ini. |
| `my-food` | `ScreenSpecs/03_MY_FOOD.md` | Melihat seluruh inventori berdasarkan urgensi. |
| `quick-add` | `ScreenSpecs/04_QUICK_ADD.md` | Menambah bahan dengan input minimal. |
| `estimate-review` | `ScreenSpecs/05_ESTIMATE_REVIEW.md` | Menjelaskan dan mengonfirmasi estimasi. |
| `food-detail` | `ScreenSpecs/06_FOOD_DETAIL.md` | Melihat alasan estimasi dan lifecycle actions. |
| `edit-food` | `ScreenSpecs/07_EDIT_FOOD.md` | Mengubah data bahan dan memicu recompute bila perlu. |
| `settings` | `ScreenSpecs/08_SETTINGS.md` | Mengatur reminder, format, privacy, dan intelligence. |
