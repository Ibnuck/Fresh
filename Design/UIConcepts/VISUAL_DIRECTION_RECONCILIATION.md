# Visual Direction Reconciliation

`fresh_ui_visual_direction.png` menunjukkan gaya yang disukai pemilik: hangat, organik, tenang, ringan, dan konsisten dengan Sprout & Slice. Gambar ini adalah referensi gaya, bukan persetujuan atas seluruh halaman atau fiturnya.

## Yang dipertahankan

- warm off-white canvas, evergreen, sage, tomato, dan amber;
- whitespace yang lapang dan hierarchy yang mudah dipindai;
- ilustrasi bahan bergaya organik dan lembut;
- surface dan control yang realistis dibuat dengan SwiftUI native;
- kesinambungan bentuk dan warna dengan ikon Sprout & Slice.

## Yang mengikuti screen spec resmi

- navigasi MVP hanya `Today`, action global `Add`, dan `My Food`; Settings berada di toolbar;
- pencarian lokal hanya pada `My Food` sesuai screen spec;
- kategori dihasilkan Fresh dan bukan input normal pengguna;
- lokasi penyimpanan, kondisi bahan, dan status kemasan menggunakan free text;
- tingkat kematangan bukan field terpisah dan boleh ditulis di kondisi bahan;
- quantity tidak wajib untuk MVP;
- copy freshness adalah estimasi dan tidak boleh menyatakan makanan pasti aman/tidak aman.

## Yang tidak diadopsi otomatis

- lima tab, tab kategori, profil, logout, kalender utama, dan halaman reminder terpisah;
- category picker atau input kategori manual;
- fitur recipe, shopping list, nutrition, cloud sync, sharing, atau analytics;
- tata letak atau copy yang bertentangan dengan file di `Fresh/Docs/ScreenSpecs/`.

## Prioritas sumber

1. Screen spec target.
2. `Fresh/Docs/DESIGN_SYSTEM.md`.
3. `Fresh/Docs/VISUAL_GENERATION_GUIDE.md`.
4. Dokumen ini.
5. `fresh_ui_visual_direction.png`.
6. Interpretasi generator.
