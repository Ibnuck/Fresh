---
concept: "02 — Sprout & Slice"
approval_status: awaiting-regenerated-foreground
updated_at: 2026-08-13
---

# Fresh Icon Composer Specification

## Composition model

Gunakan satu foreground PNG transparan yang sudah berisi daun, jam, jarum, tick, tomat, dan biji sebagai satu komposisi. Jangan memecahnya menjadi layer depan, tengah, dan belakang.

Alasan keputusan ini: tiga layer lama tidak mereplikasi konsep terpilih dengan benar. Satu artwork menyatu menjaga geometri yang telah disetujui dan membuat warna background mudah diatur langsung oleh pemilik di Icon Composer.

## Foreground requirements

- canvas `1024 × 1024 px`;
- transparent background;
- tidak memiliki rounded corner atau system mask;
- tidak memiliki background color/gradient;
- tidak memiliki shadow luar, blur, specular highlight, refraction, atau efek Liquid Glass yang dipra-render;
- seluruh elemen bergerak dan diskalakan sebagai satu unit;
- bentuk dan komposisi mengikuti `Fresh_App_Icon_Concept_02.png` sedekat mungkin.

## Icon Composer setup

Setelah artwork final disetujui:

1. Buat atau buka `Fresh/AppIcon.icon` di Apple Icon Composer.
2. Import PNG final sebagai satu foreground layer.
3. Jangan melakukan offset atau scale per-elemen karena semua elemen telah menyatu.
4. Atur warna background Default, Dark, dan Tinted di Icon Composer, bukan di PNG.
5. Gunakan depth dan material effects minimal; prioritasnya adalah fidelity terhadap konsep dan keterbacaan ukuran kecil.
6. Preview pada Default, Dark, Tinted/Mono, serta ukuran 64 px, 32 px, dan 16 px sebelum menyimpan.

## Boundary

Dokumen ini belum menyatakan ikon runtime selesai. `Fresh/AppIcon.icon` baru boleh dianggap final setelah PNG transparan hasil regenerasi diterima, dibandingkan dengan konsep, disetujui, diimpor, diekspor ulang untuk inspeksi, dan build aplikasi lolos tanpa warning ikon.
