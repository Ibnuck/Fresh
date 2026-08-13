---
concept: "02 — Sprout & Slice"
approval_status: final-and-integrated
runtime_document: ../../Fresh/AppIcon.icon
updated_at: 2026-08-13
---

# Fresh Icon Composer Specification

## Active composition

`Fresh/AppIcon.icon` adalah dokumen runtime resmi bernama `AppIcon`. Xcode sudah memiliki `ASSETCATALOG_COMPILER_APPICON_NAME = AppIcon`, sehingga nama dokumen dan build setting saling cocok.

Dokumen berisi satu group dan satu foreground layer `AppIcon_Foreground_Official`. Layer memakai master transparan lengkap; geometri daun, jam, dan tomat tidak dipecah atau diubah per-elemen. Icon Composer menyediakan shared square rendition untuk iOS/macOS dan circle preview untuk watchOS; Fresh sendiri adalah aplikasi iOS.

## Appearance yang disetujui

| Appearance | Konfigurasi final | Alasan |
|---|---|---|
| Default / Light | Automatic gradient dengan seed orange `#FF8D28` (`extended-sRGB 1.0, 0.55294, 0.15686`) | Oranye memisahkan muka jam warm-white dari bidang belakang dan tetap harmonis dengan tomat. |
| Dark | `System Dark` | Memberi pemisahan light-on-dark yang kuat tanpa menambah warna yang bersaing dengan artwork. |
| Tinted / Mono | System-controlled tint; foreground glass specialization `false` | Silhouette dan detail jarum tetap terbaca saat warna asli diganti oleh sistem. |

Jangan mengganti Default kembali ke neutral/sage terang tanpa menguji ulang kontras muka jam. Jangan bake warna appearance ke PNG.

## Liquid Glass

Liquid Glass berasal dari Icon Composer, bukan dari raster master:

- group menggunakan neutral shadow dengan opacity `0.5`;
- group translucency aktif pada nilai `0.5`;
- Default dan Dark mempertahankan depth/material response yang terlihat tetapi tidak mengaburkan gambar;
- foreground Tinted menonaktifkan glass specialization agar recoloring tidak kehilangan separation;
- tidak ada glow dramatis, refraction destruktif, atau gerakan layer yang mengubah komposisi.

Artinya ikon tetap merupakan Liquid Glass icon pada appearance utama, sementara mode Tinted memakai pengecualian yang disengaja untuk kontras.

## Bukti verifikasi visual

Eksportir resmi `ictool` berhasil membuat Default, Dark, Tinted Light, dan Tinted Dark pada `1024 × 1024`. Inspeksi visual memastikan:

- Default: batas muka jam terlihat jelas di atas oranye;
- Dark: muka jam, daun, jarum, dan tomat tetap terpisah pada bidang gelap;
- Tinted Light/Dark: struktur jam–daun–tomat dan jarum masih dikenali tanpa mengandalkan warna asli;
- tidak ada background yang bocor ke master foreground;
- komposisi tetap proporsional dan memenuhi mask sistem.

Preview hasil verifikasi bersifat artefak sementara dan tidak disimpan sebagai resource aplikasi. Bila ikon diubah, ulangi ekspor empat rendition, build aplikasi, inspeksi bundle, dan fresh reviewer gate sebelum menyatakan hasil baru final.
