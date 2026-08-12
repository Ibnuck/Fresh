---
screen_id: onboarding
screen_name: Onboarding
platform: iOS
framework: SwiftUI
target_os_design_language: iOS 26
reference_device: iPhone portrait 402x874pt
appearance: Light Mode
content_state: three-step-sequence
status: approved-for-visual-generation
version: 1
---

# Onboarding

## 1. Outcome

Pengguna memahami bahwa Fresh membantu memprioritaskan bahan yang sudah dimiliki, lalu dapat skip atau langsung menambah bahan pertama.

## 2. Entry, exit, and primary action

- Entry: launch pertama atau `Settings → Ulangi onboarding`.
- Primary actions per step: `Lanjut`, `Lanjut`, `Tambahkan bahan pertama`.
- Secondary action setiap step: `Lewati` di kanan atas.
- Exit: step 3 membuka Quick Add; skip menuju Today empty state.

## 3. Three-second hierarchy

1. Ilustrasi bahan yang sederhana dan hangat.
2. Headline manfaat, bukan daftar fitur.
3. Supporting copy maksimal tiga baris.
4. Progress 1/3, 2/3, atau 3/3.
5. CTA tunggal di bawah.

## 4. Shared top-to-bottom layout

### Region A — Status and skip

- Safe-area top; `Lewati` text button di trailing, hit area minimum 44 pt.
- Tidak ada navigation title/back pada step pertama. Step 2–3 memiliki back chevron native di leading.
- Approx. horizontal inset 20 pt.

### Region B — Illustration

- Mulai approx. 80–100 pt dari top safe area; center aligned.
- Lebar approx. 260–300 pt, tinggi maksimal 250 pt, banyak negative space.
- Gaya editorial sederhana: bentuk organik, palet sage/tomato/amber, bukan foto komersial.

### Region C — Message

- Berada 24–32 pt di bawah ilustrasi; center aligned; max width content.
- Headline `.largeTitle`/`.title`, bold, maksimal dua baris.
- Body `.body`, secondary color, maksimal tiga baris pada default size.

### Region D — Progress

- Tiga capsule/dot kecil, current step evergreen dan lebih lebar; tetap memiliki accessibility value `Langkah x dari 3`.
- Spacing 8 pt, 20–24 pt di bawah body.

### Region E — CTA dock

- Menempel secara visual ke bottom safe area dengan background canvas; bukan floating glass card.
- Full-width primary button, approx. 52 pt tinggi, horizontal inset 20 pt, bottom 12–16 pt.
- Pada Dynamic Type besar, content scroll tetapi CTA tetap dapat dicapai tanpa overlap.

## 5. Step content and exact copy

| Step | Illustration concept | Headline | Body | CTA |
|---|---|---|---|---|
| 1 | Berbagai sayur di meja dapur, satu bahan sedikit tersembunyi | `Masak dengan yang sudah ada` | `Fresh membantu melihat bahan mana yang sebaiknya dipakai lebih dulu.` | `Lanjut` |
| 2 | Bayam dan susu dengan label waktu lembut, bukan alarm | `Tidak ada lagi bahan terlupakan` | `Dapatkan pengingat yang tenang sebelum bahan melewati perkiraan terbaiknya.` | `Lanjut` |
| 3 | Satu kartu bahan dengan countdown dan tombol tambah | `Mulai dari satu bahan` | `Tambahkan yang ada di kulkas. Kamu tetap mengendalikan setiap estimasi.` | `Tambahkan bahan pertama` |

Secondary exact copy: `Lewati`.

## 6. Component inventory

| Component | SwiftUI mapping | Interaction |
|---|---|---|
| Page container | `TabView` page style atau controlled state | Horizontal transition; swipe opsional, CTA utama. |
| Skip/back | `Button` in safe-area header | Skip exits; back changes step. |
| Illustration | `Image`/vector asset | Decorative; hidden from VoiceOver unless conveying unique info. |
| Progress | custom `HStack` of capsules | Non-interactive; announces step count. |
| CTA | `Button` prominent style | Advances or presents Quick Add sheet. |

## 7. Interaction and states

- Preserve current step if app briefly backgrounds during onboarding.
- Reduce Motion: cross-fade; no large parallax.
- Error state tidak diperlukan karena onboarding local-only.
- Dark Mode: canvas near-black green, illustration colors softened, CTA brand remains high contrast.
- Large Dynamic Type: illustration dapat menyusut/hilang sebagian; message dan CTA tidak terpotong.

## 8. Accessibility

- VoiceOver order: skip/back → headline → body → progress → CTA.
- Jangan membaca ilustrasi dekoratif sebagai `image` tanpa makna.
- CTA labels berdiri sendiri dan tidak hanya `Next` tanpa konteks pada step akhir.

## 9. Do not include

- Permission notification prompt, account/login, paywall, statistics, carousel feature list, atau recipe imagery.
- Klaim persentase pengurangan food waste yang tidak didukung.

## 10. Requested outputs

- `onboarding_step1_light_v01.png`
- `onboarding_step2_light_v01.png`
- `onboarding_step3_light_v01.png`
- Satu proposal Markdown yang menjelaskan continuity ketiga step.
