---
concept: "02 — Sprout & Slice"
approval_status: approved-visual-reference / artwork-regeneration-required
reference: Fresh_App_Icon_Concept_02.png
updated_at: 2026-08-13
---

# Fresh App Icon Artwork Specification

## Status

`Fresh_App_Icon_Concept_02.png` adalah sumber visual resmi untuk bentuk ikon. Artwork lama yang dipisah menjadi `01_back`, `02_middle`, dan `03_front` tidak sama dengan gambar konsep dan tidak boleh dipakai sebagai master.

Ikon final belum tersedia. Langkah berikutnya adalah menghasilkan ulang satu PNG foreground transparan yang mereplikasi simbol pada konsep sedekat mungkin.

## Target output

- satu file PNG `1024 × 1024 px`;
- background benar-benar transparan;
- sRGB dan alpha yang bersih;
- tanpa rounded-square plate, mask iOS, warna background, shadow luar, teks, atau device mockup;
- seluruh simbol sudah menyatu dalam satu artwork, bukan file depan/tengah/belakang;
- ruang transparan di sekeliling simbol cukup untuk pengaturan scale di Icon Composer.

Warna background Default, Dark, dan Tinted akan ditentukan secara terpisah oleh pemilik di Apple Icon Composer.

## Fidelity requirement

Artwork harus mengikuti simbol besar di sisi kiri gambar konsep dan preview `FINAL APP ICON (COMPOSED)`, bukan menafsirkan ulang idenya. Pertahankan sedekat mungkin:

- silhouette, sudut, ukuran relatif, overlap, dan optical balance;
- dua daun di atas jam: daun kiri hijau tua dan daun kanan hijau muda;
- muka jam warm off-white berbentuk lingkaran tanpa outline;
- jarum jam hijau tua berbentuk L dengan ujung membulat;
- dua tick kecil hijau tua;
- irisan tomat oranye-merah yang menimpa bagian kanan bawah jam;
- tiga biji besar berwarna kuning hangat;
- gaya flat-organic yang lembut dengan depth/tonal variation tipis seperti konsep.

Jangan mengubah proporsi, mengganti posisi elemen, menambah detail, atau membuat versi baru yang sekadar "terinspirasi" oleh konsep.

## Palette reference

Gunakan warna yang tampak pada gambar konsep sebagai sumber utama. Token berikut membantu konsistensi, tetapi visual match terhadap referensi lebih penting daripada memaksakan hex bila gambar memiliki tonal variation:

| Role | Direction |
|---|---|
| Evergreen | `#1F6B4F` |
| Pale leaf | sekitar `#8FBD6D` |
| Warm off-white | `#F7F5EF` |
| Tomato | sekitar `#E45A3E` |
| Seed yellow | sekitar `#FFD58A` |

Tidak ada warna background dalam PNG final.

## Review checklist

- overlay comparison terhadap simbol pada konsep tidak menunjukkan pergeseran bentuk atau proporsi yang jelas;
- jam, daun, jarum, tick, tomat, dan tiga biji tetap terbaca pada 64 px dan 32 px;
- tepi alpha bersih dan tidak memiliki halo warna background;
- tidak ada elemen concept board yang ikut terpotong ke artwork;
- file dapat diimpor sebagai satu foreground layer ke Icon Composer.
