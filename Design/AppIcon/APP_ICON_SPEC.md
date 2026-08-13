---
concept: "02 — Sprout & Slice"
approval_status: final-and-integrated
official_foreground: AppIcon_Foreground_Official.png
runtime_document: ../../Fresh/AppIcon.icon
updated_at: 2026-08-13
---

# Fresh App Icon Artwork Specification

## Status

`AppIcon_Foreground_Official.png` adalah master artwork resmi yang dipilih pemilik dari kandidat `3.png`. File ini menggantikan concept board sebagai sumber produksi. `Fresh_App_Icon_Concept_02.png` tetap disimpan sebagai referensi historis yang mengarahkan generasi, bukan sebagai input runtime.

Ikon runtime sudah selesai di `Fresh/AppIcon.icon`. Jangan menghasilkan ulang atau mengganti artwork kecuali pemilik membuat keputusan baru yang dicatat di decision log.

## Properti master

- ukuran asli `1230 × 1223 px`;
- PNG RGBA dengan background transparan;
- SHA-256 `ae398ad3ecd1f3f2d2cadc411715115d9db41a67e46afc0d55ea9b55967e0d76`;
- satu komposisi utuh berisi daun, jam, jarum, tick, tomat, dan tiga biji;
- tidak memiliki rounded-square plate atau warna background yang dipra-render;
- harus dipasang secara proporsional sebagai satu unit—jangan stretch, crop, pecah menjadi layer baru, atau mengubah posisi relatif elemen.

Salinan di dalam `Fresh/AppIcon.icon/Assets/AppIcon_Foreground_Official.png` harus tetap byte-identical dengan master ini.

## Bentuk dan identitas

- dua daun di atas jam: kiri hijau tua dan kanan hijau muda;
- muka jam warm off-white;
- jarum jam hijau tua berbentuk L dengan ujung membulat;
- dua tick kecil hijau tua;
- irisan tomat oranye-merah menimpa kanan bawah jam;
- tiga biji besar berwarna kuning hangat;
- gaya flat-organic lembut dengan tonal variation, highlight, dan kedalaman ringan.

## Keterbacaan

Warna background bukan bagian dari PNG. Mode Default memakai oranye agar muka jam terang tidak bertabrakan dengan background; Dark dan Tinted diselesaikan oleh Icon Composer. Semua mode harus mempertahankan silhouette daun–jam–tomat serta jarum jam pada ukuran Home Screen kecil.

## Hubungan dengan desain halaman

Ikon adalah identitas aplikasi, bukan ilustrasi generik. Desain layar dan ilustrasi transparan boleh mengambil karakter organik, bentuk membulat, palet hijau–tomat–kuning, dan kedalaman lembutnya. Jangan menempelkan atau menggambar ulang ikon lengkap pada setiap hero, empty state, atau card.
