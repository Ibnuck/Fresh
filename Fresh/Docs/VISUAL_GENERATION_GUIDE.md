# Visual Generation Guide

## Purpose

Panduan ini mengubah screen spec menjadi mockup UI dan proposal Markdown yang dapat ditinjau sebelum coding. Gambar adalah proposal visual; screen spec tetap sumber kebenaran sampai perubahan disetujui.

## Required inputs

Untuk satu tugas visual, selalu baca:

1. `VISUAL_HANDOFF_README.md`.
2. `DESIGN_SYSTEM.md`.
3. Screen spec target.
4. Screen spec asal/tujuan bila flow antarlayar perlu terlihat.

Jangan meminta histori chat kecuali file-file tersebut benar-benar tidak menjawab keputusan material.

## Generation protocol

### Step 1 — Restate the target

Sebelum menghasilkan gambar, tulis ringkasan singkat:

- screen dan state;
- primary action;
- tiga elemen visual terpenting;
- batas yang tidak boleh dilanggar.

### Step 2 — Compose the screen

- Ikuti urutan region di screen spec dari atas ke bawah.
- Pertahankan native safe area, navigation bar, sheet detent, keyboard state, dan tab bar yang disebut.
- Gunakan contoh data persis agar continuity antarhalaman terjaga.
- Jika ruang tidak cukup, prioritaskan primary action dan informasi kritis; scroll konten sekunder secara vertikal.

### Step 3 — Produce variants only when requested

- Default: satu gambar Light Mode populated/default state.
- Buat Dark Mode, empty, error, loading, atau Dynamic Type hanya jika `requested_outputs` memintanya.
- Jangan membuat style alternatif A/B tanpa diminta.

### Step 4 — Self-check before delivery

Periksa:

- Ini jelas aplikasi iOS, bukan web/Android?
- Primary action terbaca dalam 3 detik?
- Semua copy sesuai spec?
- Status memakai teks selain warna?
- Layout realistis untuk SwiftUI dan Dynamic Type?
- Tidak ada fitur baru atau klaim food safety?
- Tab/navigation position sesuai flow?

### Step 5 — Write the proposal Markdown

Gunakan `VisualReferences/GENERATED_UI_PROPOSAL_TEMPLATE.md`. Sertakan path/nama gambar, keputusan layout, tokens, component mapping, state behavior, accessibility, dan seluruh deviasi.

## Image prompt skeleton

```text
Create a high-fidelity native iOS SwiftUI screen mockup for the Fresh food
freshness app. Device: iPhone portrait, 402x874 pt, [Light/Dark] Mode.
Screen: [name]. State: [state]. Primary action: [action].

Visual character: calm organic minimalism with clinical clarity; warm off-white
canvas, restrained evergreen brand accents, natural food imagery, native San
Francisco typography, realistic iOS navigation and controls. Follow the supplied
top-to-bottom regions, exact Indonesian UI copy, spacing hierarchy, and example
data. Urgency must use text/icon plus color.

Do not create a website, Android UI, dashboard, recipe app, shopping list,
nutrition score, excessive glass, neon, heavy gradients, nested cards, or food
safety guarantees. Do not add features or copy not present in the specification.
```

Tambahkan detail screen spec setelah skeleton tersebut, bukan menggantinya dengan interpretasi bebas.

## Required visual annotation in Markdown

Untuk setiap major region jelaskan:

- bounding position: top/middle/bottom dan hubungan ke safe area;
- width: full content width, intrinsic, atau proportional;
- height behavior: fixed/minimum/content-driven;
- alignment dan spacing;
- component semantics dan planned SwiftUI primitive;
- behavior saat scroll, keyboard, Dynamic Type, empty/error, dan Dark Mode;
- accessibility name/value/hint bila interaktif.

Gunakan ukuran dalam point sebagai intent, bukan pixel-perfect contract. Sebut `approx.` untuk angka visual yang dapat berubah ketika Dynamic Type aktif.

## Continuity dataset

Gunakan data berikut kecuali screen spec meminta state lain:

| Item | Storage | Reference | Status | Countdown |
|---|---|---|---|---|
| Bayam | Kulkas | Dicuci, dibuka | Use Today | Hari ini |
| Susu segar | Kulkas | Dibuka kemarin | Use Soon | 2 hari |
| Tempe | Kulkas | Kemasan tertutup | Fresh | 4 hari |
| Alpukat | Dekat jendela | Lokasi belum dipahami Fresh | Needs Review | Tinjau |

## Handling ambiguity

- Bila ambiguity kecil: pilih interpretasi native paling sederhana dan catat di `Assumptions`.
- Bila ambiguity mengubah navigation, feature scope, safety wording, data model, atau primary action: jangan memutuskan diam-diam. Tandai `Decision needed` dalam Markdown.
- Jangan mengubah screen spec asli.

## Deliverables

1. Mockup image(s) dengan nama: `{screen_id}_{state}_{appearance}_v01.png`.
2. Satu Markdown proposal: `{screen_id}_GENERATED_UI_PROPOSAL.md`.
3. Tabel compliance: requirement, met/not met, note.
4. Daftar deviasi dan pertanyaan keputusan.
