# Fresh Design System

## 1. Design intent

Fresh harus terasa seperti asisten dapur iPhone yang tenang, hangat, jujur, dan cepat dipindai. Komposisi visual:

- 70% Organic Minimalism: ruang lapang, warna natural, bentuk lembut.
- 20% Clinical Clarity: hierarchy tegas, label eksplisit, estimasi transparan.
- 10% Playful Food Personality: ilustrasi/foto bahan dan microcopy ramah.

Hindari estetika dashboard enterprise, aplikasi medis, toko online, atau game.

## 2. Target canvas

- Platform: iOS native SwiftUI.
- Primary frame: iPhone portrait 402 × 874 pt.
- Respect safe areas dan system status bar.
- Gunakan navigation bar dan bottom tab bar native.
- Base spacing grid: 4 pt; jarak utama 8, 12, 16, 20, 24, dan 32 pt.
- Horizontal content inset utama: 20 pt.
- Minimum interactive hit target: 44 × 44 pt.
- Preferred corner radii: 12 pt untuk field/small surface, 16 pt untuk cards, pill penuh hanya untuk chips/status.

## 3. Color roles

Nilai berikut adalah arahan awal, bukan kewajiban memakai hex persis saat implementasi native. Pastikan kontras dapat diakses.

| Token | Light direction | Dark direction | Usage |
|---|---|---|---|
| `canvas` | warm off-white `#F7F5EF` | near-black green `#111612` | Background utama. |
| `surface` | white `#FFFFFF` | charcoal green `#1B211D` | Sheet, card terpilih, grouped surface. |
| `textPrimary` | ink `#18201B` | warm white `#F3F5F1` | Judul dan isi utama. |
| `textSecondary` | muted olive gray `#667068` | gray green `#AAB3AC` | Metadata dan penjelasan. |
| `brand` | evergreen `#1F6B4F` | softened mint-green `#5DBB8E` | CTA utama, selected state, focus. |
| `brandSoft` | pale sage `#DDEADF` | deep sage `#244232` | Background brand ringan. |
| `useToday` | tomato `#C94B3B` | warm coral `#F27868` | Urgensi tertinggi; selalu dengan teks/ikon. |
| `useSoon` | amber `#B66B13` | golden amber `#E7A542` | Perlu segera; selalu dengan teks/ikon. |
| `fresh` | leaf green `#4B7D45` | light leaf `#81BE78` | Kondisi masih fresh. |
| `needsReview` | slate blue `#58708A` | light slate `#91A9C1` | Data perlu ditinjau. |
| `divider` | `#E4E5DF` | `#343B36` | Separator tipis. |

Jangan memenuhi seluruh layar dengan hijau. Brand color idealnya muncul pada CTA, highlight, icon, dan beberapa surface ringan.

## 4. Typography

Gunakan San Francisco melalui Dynamic Type, bukan font dekoratif eksternal.

| Role | Native style | Visual intent |
|---|---|---|
| Screen title | `.largeTitle`, bold | Fokus halaman; maksimal dua baris. |
| Section title | `.title3`, semibold | Kelompok informasi utama. |
| Card hero value | `.title` atau `.largeTitle`, bold rounded bila cocok | Countdown atau nilai utama. |
| Body | `.body` | Instruksi dan isi. |
| Supporting | `.subheadline` | Metadata penting sekunder. |
| Caption | `.caption` | Source, confidence, hint; jangan untuk informasi kritis. |
| Button | `.headline` | CTA mudah dikenali. |

Jangan mengecilkan teks hanya agar muat. Pada Dynamic Type besar, layout harus tumbuh vertikal dan HStack boleh berubah menjadi VStack.

## 5. Iconography and food imagery

- Gunakan SF Symbols untuk navigation/action: `plus`, `gearshape`, `magnifyingglass`, `snowflake`, `checkmark`, `trash`, `pencil`, `bell`.
- Ikon tidak menjadi satu-satunya label untuk action yang ambigu.
- Foto makanan, bila dipakai, memakai crop natural dengan pencahayaan lembut; jangan glossy seperti iklan restoran.
- Jika tidak ada foto, gunakan illustration/shape sederhana dengan satu bahan utama, bukan emoji besar.
- Hero illustration harus menyisakan ruang untuk teks dan tidak mendominasi lebih dari sekitar 35% tinggi layar.
- Ikon final Sprout & Slice di `../AppIcon.icon` adalah identitas aplikasi, bukan ilustrasi hero generik. Ilustrasi halaman boleh memakai bahasa bentuk organik, palet hijau–tomat–kuning, dan depth lembut yang selaras, tetapi jangan menyalin komposisi daun–jam–tomat lengkap pada setiap layar.

## 6. Core components

### Primary button

- Full-width di form/onboarding; dapat inline pada toolbar hanya untuk action pendek.
- Tinggi visual sekitar 50–54 pt.
- Brand fill, high-contrast label, 14–16 pt radius.
- Hanya satu CTA utama dominan per viewport.

### Secondary button

- Tinted/outline atau text button native.
- Jangan terlihat lebih kuat daripada primary CTA.

### Urgency badge

- Pill kecil berisi icon opsional + teks (`Use Today`, `Use Soon`, `Fresh`, `Needs Review`).
- Tone background lembut, foreground kontras.
- Jangan hanya berupa dot warna.

### Food row

- Minimum height 72 pt pada ukuran teks default.
- Leading: thumbnail 48–56 pt atau fallback icon.
- Center: nama, metadata storage/date, status text.
- Trailing: countdown atau disclosure; bukan lebih dari dua elemen.
- Seluruh row dapat ditekan; swipe actions tidak menjadi satu-satunya cara melakukan lifecycle action.

### Information card

- Satu card mewakili satu keputusan/informasi, bukan sekadar dekorasi.
- Padding 16 pt, radius 16 pt, border/shadow sangat halus.
- Maksimal satu level card; jangan card di dalam card.

### Input row

- Label terlihat, value/input di bawah atau trailing sesuai panjang.
- Unknown diperlihatkan sebagai `Belum dipilih`, bukan default palsu.
- Validation dan error ditempatkan dekat input terkait.

### Bottom tab bar

- Tiga tujuan visual: `Today`, global `Add`, `My Food`.
- `Add` boleh menjadi action pusat yang menonjol, tetapi tetap tampak native dan tidak seperti floating web button.
- Settings di toolbar, bukan tab keempat untuk MVP.

## 7. Motion and feedback

- Animasi singkat 150–300 ms untuk insert, regroup, dan state transition.
- Hormati Reduce Motion dengan fade atau tanpa perpindahan besar.
- Gunakan haptic ringan hanya pada save/lifecycle action sukses, tidak pada setiap tap.
- Jangan membuat countdown berdenyut atau memakai animasi kecemasan.

## 8. Accessibility rules

- Kontras teks normal minimal 4.5:1 sebagai target.
- Status memiliki teks dan bukan warna saja.
- Food row VoiceOver menggabungkan: nama, status, perkiraan waktu, storage.
- Button icon-only harus punya accessibility label yang berupa kata kerja.
- Urutan fokus mengikuti layout atas ke bawah.
- Dynamic Type accessibility sizes tidak memotong CTA atau countdown.
- Jangan menyembunyikan informasi penting dalam tooltip/hover.
- Gunakan bahasa estimasi: `diperkirakan`, `berdasarkan`, `perlu ditinjau`.

## 9. Global copy voice

- Singkat, aktif, menenangkan, tidak menghakimi.
- Utamakan tindakan: `Gunakan hari ini`, `Tambahkan bahan`, `Sesuaikan estimasi`.
- Hindari: `Kamu membuang makanan`, `Bahaya`, atau klaim pasti.
- Bahasa utama mockup: Bahasa Indonesia. Nama token/status internal boleh bahasa Inggris di metadata saja.

## 10. Global do-not list

- Tidak ada glassmorphism berat, neon, gradient mencolok, atau shadow tebal.
- Tidak ada sidebar, multi-column desktop, chart dashboard, score gamification, atau feed sosial.
- Tidak ada floating cards berlapis tanpa fungsi.
- Tidak ada recipe, shopping list, nutrition grade, harga, komunitas, atau iklan pada MVP.
- Jangan menggambar kontrol yang tidak realistis dibuat di SwiftUI/native iOS.
