# Fresh: Food Countdown — UI/UX Design Research

> Status: research brief awal, belum menjadi keputusan desain final<br>
> Tanggal: 12 Agustus 2026<br>
> Platform awal: iOS / SwiftUI

## 1. Ringkasan Eksekutif

Fresh sebaiknya tidak tampil seperti aplikasi medis, aplikasi diet, atau spreadsheet inventaris. Posisi visual yang paling sesuai adalah **organic minimalism**: bersih, terang, tenang, alami, dan tetap membuat makanan terlihat menggugah selera.

Rekomendasi awal:

- Gunakan **hijau tua yang matang** sebagai warna brand dan mint pucat sebagai warna pendukung, bukan memenuhi seluruh layar dengan hijau.
- Pertahankan kanvas netral seperti putih hangat atau off-white agar foto dan warna alami makanan menjadi pusat perhatian.
- Gunakan amber dan merah-tomat secara terbatas untuk menyatakan urgensi kedaluwarsa.
- Jadikan **countdown dan tindakan berikutnya** sebagai pusat hierarki, bukan jumlah data yang berhasil disimpan.
- Gunakan bahasa yang membantu dan tidak menghakimi: “Gunakan hari ini”, “Masih sempat dibekukan”, atau “Sudah lewat 1 hari”, bukan pesan yang menimbulkan rasa bersalah.
- Jangan menyamakan “belum kedaluwarsa” dengan “sehat”. Fresh mengelola kesegaran dan waktu konsumsi; klaim nutrisi adalah domain berbeda.

Arah yang disarankan adalah perpaduan kira-kira **70% Organic Minimal, 20% Clinical Clarity, dan 10% Playful Food Personality**. Hasilnya harus terasa sehat dan terpercaya, tetapi tetap hangat serta dekat dengan kehidupan sehari-hari.

---

## 2. Apa yang Secara Visual Menggambarkan Kesehatan, Kesegaran, dan Makanan?

### 2.1 Kesehatan

Kesan sehat biasanya muncul dari kombinasi berikut:

- ruang kosong yang cukup dan struktur yang tidak sesak;
- tipografi yang mudah dibaca;
- warna alami dengan saturasi terkontrol;
- bentuk membulat yang ramah, tetapi tidak kekanak-kanakan;
- informasi yang transparan dan mudah dipahami;
- tone of voice yang tenang, suportif, dan tidak menakut-nakuti;
- interaksi yang terasa stabil, dapat diprediksi, dan tidak berlebihan.

Kesehatan bukan hanya persoalan warna hijau. Antarmuka yang penuh, membingungkan, atau memiliki kontras rendah tetap terasa “tidak sehat” walaupun seluruh komponennya berwarna hijau.

### 2.2 Kesegaran

Kesegaran paling kuat dikomunikasikan melalui:

- foto makanan dengan pencahayaan alami;
- palet botanical: hijau daun, mint, putih hangat, warna buah dan sayur;
- komposisi yang lapang;
- bentuk organik ringan seperti lingkaran, kapsul, daun, atau kurva lembut;
- microcopy aktif seperti “Segar 4 hari lagi” dan “Gunakan berikutnya”;
- motion yang ringan dan responsif, bukan animasi berat;
- pembaruan status yang terasa hidup dan tepat waktu.

Riset tentang warna kemasan menunjukkan bahwa hijau dan putih umum diasosiasikan dengan produk organik, sehat, dan segar. Namun efek warna bergantung pada konteks dan budaya, sehingga warna perlu didukung oleh teks, ikon, dan struktur informasi, bukan dipakai sebagai satu-satunya sinyal.

### 2.3 Makanan

Kesan makanan sebaiknya datang dari konten makanan itu sendiri:

- foto produk atau ilustrasi bahan pangan yang realistis dan bersih;
- warna aksen yang berasal dari bahan makanan, misalnya tomat, jeruk, berry, atau kunyit;
- kategori yang mudah dikenali melalui nama dan ikon;
- bahasa yang konkret: “Susu”, “Bayam”, “Sisa rendang”, bukan label teknis yang dingin;
- aksi yang relevan dengan dapur: gunakan, masak, bekukan, bagikan, habiskan, atau buang.

Hindari menggunakan terlalu banyak warna kategori secara bersamaan. Foto makanan sudah menghasilkan variasi visual; UI perlu menjadi bingkai yang tenang.

---

## 3. Tiga Arah Style yang Mungkin Digunakan

### A. Organic Minimalism — Rekomendasi

**Karakter:** bersih, alami, premium tetapi tidak mewah, hangat, ringan.

**Ciri visual:**

- off-white sebagai kanvas utama;
- evergreen sebagai warna brand;
- foto makanan dengan rasio dan pencahayaan konsisten;
- kartu putih dengan border halus, bukan bayangan berat;
- radius sedang hingga besar;
- tipografi sistem yang bersih;
- ilustrasi botanical hanya sebagai aksen.

**Kelebihan:** paling seimbang untuk menyampaikan kesehatan, kesegaran, dan makanan; mudah dikembangkan menjadi design system; konten tetap menjadi pusat perhatian.

**Risiko:** dapat terasa generik jika tidak memiliki bentuk khas, tone of voice, atau treatment foto yang konsisten.

### B. Clinical Wellness

**Karakter:** presisi, aman, terpercaya, informatif.

**Ciri visual:**

- putih dan warna netral dominan;
- hijau atau biru sebagai aksen terukur;
- data, label, dan status sangat terstruktur;
- ikon sederhana dan hampir tanpa dekorasi;
- grafik serta metrik menjadi elemen utama.

**Kelebihan:** bagus untuk kejelasan countdown, status, dan aksesibilitas; terasa dapat dipercaya.

**Risiko:** dapat terasa seperti aplikasi rumah sakit, nutrisi, atau laboratorium; makanan kehilangan kehangatan dan daya tarik.

### C. Playful Farmers Market

**Karakter:** ceria, manusiawi, lokal, penuh energi.

**Ciri visual:**

- ilustrasi buah dan sayur;
- palet multiwarna;
- bentuk organik dan tipografi lebih ekspresif;
- empty state serta achievement yang menyenangkan.

**Kelebihan:** mudah diingat, ramah untuk keluarga, dan cocok untuk membangun kebiasaan positif.

**Risiko:** terlalu banyak warna dapat mengaburkan status kedaluwarsa; berpotensi terlihat kekanak-kanakan dan kurang premium.

### Rekomendasi Campuran

Gunakan **Organic Minimalism sebagai fondasi**, ambil ketelitian informasi dari **Clinical Wellness**, lalu tambahkan ilustrasi atau copy ringan dari **Playful Farmers Market** pada onboarding, empty state, dan celebration. Jangan mencampur ketiganya dengan bobot yang sama.

---

## 4. Arah Warna

### 4.1 Prinsip Warna

1. Hijau berfungsi sebagai identitas brand dan aksi positif, bukan sebagai warna seluruh permukaan.
2. Warna status harus semantik dan konsisten.
3. Status tidak boleh disampaikan lewat warna saja; selalu sertakan label, ikon, bentuk, atau posisi.
4. Foto makanan boleh menjadi sumber warna paling kaya di layar.
5. Semua warna perlu memiliki varian Light Mode, Dark Mode, Increase Contrast, dan kondisi disabled.
6. Gunakan semantic color assets di Xcode, bukan nilai warna yang tersebar langsung di view.

### 4.2 Kandidat Palet Awal

| Token konseptual | Nilai awal | Fungsi |
|---|---:|---|
| Brand Evergreen | `#1F6B4F` | Tombol utama, highlight brand, ikon aktif |
| Brand Strong | `#17573F` | State pressed, teks brand dengan kontras lebih tinggi |
| Fresh Mint | `#EAF6EF` | Background lembut, selected state ringan |
| Canvas | `#F7FAF7` | Latar utama Light Mode |
| Surface | `#FFFFFF` | Kartu, sheet, field |
| Text Primary | `#152019` | Judul dan body utama |
| Text Secondary | `#56635B` | Metadata dan deskripsi sekunder |
| Warning Amber | `#9A5A00` | “Segera digunakan” |
| Urgent Tomato | `#B5473E` | Kedaluwarsa atau tindakan mendesak |

Nilai ini adalah kandidat awal, bukan token produksi final. Pada permukaan putih, Brand Evergreen, Text Primary, Text Secondary, Warning Amber, dan Urgent Tomato memiliki rasio kontras di atas 4.5:1. Pasangan warna lain tetap perlu diuji secara individual.

### 4.3 Semantik Status Countdown

| Status | Warna pendukung | Label contoh | Ikon/bentuk |
|---|---|---|---|
| Fresh | Hijau | `Masih 8 hari` | checkmark / badge lembut |
| Use soon | Amber | `Gunakan dalam 2 hari` | jam / badge ber-outline |
| Use today | Oranye-tomat | `Gunakan hari ini` | timer / badge solid ringan |
| Expired | Merah tua | `Lewat 1 hari` | tanda seru / bar status |
| Unknown | Abu netral | `Tanggal belum diisi` | kalender bertanda tanya |

Ambang batas sebaiknya dapat menyesuaikan jenis makanan. “2 hari lagi” untuk sayuran segar tidak selalu memiliki urgensi yang sama dengan makanan beku.

---

## 5. Penerapan 12 Prinsip Desain

Tidak ada satu daftar “12 prinsip desain” yang universal. Untuk Fresh, dokumen ini menggunakan: **balance, contrast, emphasis, hierarchy, proportion, repetition, rhythm, pattern, movement, white space, variety, dan unity**.

| Prinsip | Penerapan pada Fresh | Hal yang perlu dihindari |
|---|---|---|
| Balance | Seimbangkan ringkasan countdown, daftar makanan, dan ruang kosong. Dashboard boleh asimetris selama bobot visual tetap stabil. | Semua kartu memiliki bobot sama sehingga layar terasa seperti grid spreadsheet. |
| Contrast | Bedakan aksi utama, teks penting, dan tingkat urgensi melalui nilai warna, ukuran, weight, serta bentuk. | Mengandalkan hijau-kuning-merah saja. |
| Emphasis | Berikan fokus tertinggi pada item yang perlu digunakan terlebih dahulu dan satu tindakan yang paling relevan. | Banyak CTA berwarna solid pada satu layar. |
| Hierarchy | Urutan baca: countdown → nama makanan → tindakan → lokasi dan metadata. | Metadata kecil bersaing dengan countdown utama. |
| Proportion | Countdown memakai skala lebih besar; foto dan kartu menyesuaikan pentingnya informasi. | Foto sangat besar tetapi tindakan penting tersembunyi. |
| Repetition | Gunakan struktur kartu, badge, ikon, radius, dan spacing yang konsisten. | Membuat style baru untuk setiap kategori makanan. |
| Rhythm | Gunakan pola spacing vertikal yang konsisten agar daftar mudah dipindai. | Jarak acak dan density yang berubah-ubah. |
| Pattern | Pola interaksi sama untuk consume, freeze, edit, dan discard di semua daftar. | Swipe memiliki arti berbeda pada layar berbeda tanpa petunjuk. |
| Movement | Arahkan mata dari ringkasan ke kelompok “Hari ini”, lalu “Berikutnya”; gunakan motion untuk menjelaskan perubahan status. | Animasi dekoratif yang menghambat pencatatan cepat. |
| White Space | Beri napas di sekitar countdown, judul kelompok, dan CTA. | Memenuhi layar dengan insight, promo, dan statistik sekaligus. |
| Variety | Variasi datang dari foto makanan, ilustrasi kecil, dan state; fondasi layout tetap stabil. | Semua elemen dibuat berbeda agar terlihat “seru”. |
| Unity | Seluruh layar memakai token, komponen, bahasa, dan pola interaksi yang sama. | Onboarding terasa playful tetapi aplikasi utama terasa klinis tanpa jembatan visual. |

Prinsip-prinsip tersebut berfungsi sebagai alat evaluasi, bukan checklist dekorasi. Sebuah layar tidak harus menonjolkan seluruh prinsip secara sama kuat.

---

## 6. Prinsip UX yang Disarankan

### 6.1 Countdown-first, bukan inventory-first

Pertanyaan utama pengguna bukan “Berapa banyak item saya?”, melainkan:

- Apa yang harus saya gunakan lebih dulu?
- Apa yang bisa saya masak hari ini?
- Apa yang perlu dibekukan?
- Apa yang sudah terlambat?

Beranda harus menjawab pertanyaan tersebut dalam beberapa detik.

### 6.2 Action-first

Setiap item mendukung tindakan kontekstual yang jelas:

- `Gunakan`
- `Bekukan`
- `Tambah waktu`
- `Pindahkan`
- `Bagikan`
- `Buang`

Tindakan destruktif perlu confirmation atau undo. Tindakan yang paling aman dan sering dipakai harus paling mudah dijangkau.

### 6.3 Calm urgency

Fresh perlu menciptakan urgensi tanpa kecemasan. Gunakan kalimat faktual dan dapat ditindaklanjuti. Warna merah hanya untuk kondisi yang memang membutuhkan perhatian, bukan untuk menghukum pengguna.

### 6.4 Input harus sangat cepat

Nilai aplikasi bergantung pada kemauan pengguna mencatat makanan. Karena itu, alur tambah harus mendukung:

- scan barcode;
- foto atau deteksi label;
- preset tanggal seperti `3 hari`, `1 minggu`, atau `akhir bulan`;
- recent items dan duplicate/re-add;
- contoh singkat pada text field lokasi penyimpanan;
- edit detail secara progresif, bukan semua field di awal.

Ulasan pengguna FridgeBuddy secara spesifik menunjukkan pentingnya re-adding item yang sering dibeli dan shortcut tanggal kedaluwarsa. Ini adalah sinyal bahwa friction pencatatan lebih penting daripada banyaknya fitur.

### 6.5 Recognition over recall

Gunakan foto, nama, kategori, dan lokasi yang mudah dikenali. Jangan meminta pengguna mengingat struktur storage atau aturan tanggal yang pernah mereka masukkan.

### 6.6 Progressive disclosure

Tampilkan hanya informasi yang dibutuhkan untuk mengambil keputusan. Nutrisi, riwayat perubahan, harga, dan catatan dapat berada di detail, bukan memenuhi daftar utama.

### 6.7 Accessible by default

- Target minimum kontras teks normal: `4.5:1`.
- Target kontras komponen dan state nonteks: `3:1`.
- Jangan gunakan warna sebagai satu-satunya pembeda.
- Dukung Dynamic Type tanpa clipping.
- Gunakan label VoiceOver yang menyebut nama, status countdown, lokasi, dan tindakan.
- Hormati Reduce Motion, Increase Contrast, dan pilihan Light/Dark Mode sistem.
- Pertahankan target sentuh yang nyaman dan jarak antartindakan yang cukup.

---

## 7. Benchmark Aplikasi Serupa

### 7.1 FridgeBuddy

Fokus pada barcode, tanggal kedaluwarsa, lokasi penyimpanan, household sharing, shopping list, insight, Nutri-Score, dan Green-Score.

**Pelajaran untuk Fresh:**

- expiry alert dan lokasi adalah kebutuhan dasar;
- shortcut tanggal dan re-add item sangat penting;
- terlalu banyak kapabilitas berisiko mengubah produk menjadi sistem inventaris yang berat;
- Fresh dapat berbeda dengan berfokus pada tindakan “use next”.

### 7.2 NoWaste

Mengorganisasi freezer, fridge, dan pantry; mendukung expiry tracking, barcode, photo recognition, recipe, dan shopping list.

**Pelajaran untuk Fresh:**

- storage location adalah mental model yang sudah dikenal;
- scan dan recognition mengurangi biaya input;
- resep berguna jika muncul dari bahan yang mendekati kedaluwarsa, bukan menjadi modul besar sejak versi pertama.

### 7.3 Pantry Check

Menggabungkan barcode scanning, sinkronisasi keluarga, expiration reminder, smart shopping list, lokasi, harga, dan timeline penggunaan.

**Pelajaran untuk Fresh:**

- household sync dapat menjadi nilai besar;
- fitur inventory dan budget cepat memperluas scope;
- visual hierarchy harus melindungi tugas utama dari kepadatan fitur.

### 7.4 FoodShiner

Menawarkan storage lists, SmartLists untuk expiring/expired/opened, iCloud sharing, recipes, shopping list, dan pendekatan privasi tanpa akun wajib.

**Pelajaran untuk Fresh:**

- SmartLists berdasarkan waktu adalah pola yang kuat;
- local-first/iCloud cocok dengan ekspektasi pengguna ekosistem Apple;
- dukungan terhadap desain platform terbaru tetap perlu disesuaikan dengan identitas brand, bukan sekadar mengikuti efek visual sistem.

### 7.5 Yuka — Referensi dari Domain Kesehatan

Yuka bukan expiry tracker, tetapi berhasil menyederhanakan analisis kompleks menjadi rating yang cepat dipahami dan rekomendasi alternatif.

**Pelajaran untuk Fresh:**

- ringkasan harus dapat dipahami dalam satu pandangan;
- status perlu selalu disertai penjelasan;
- setelah menunjukkan masalah, berikan tindakan atau alternatif;
- jangan membuat klaim kesehatan yang tidak dapat dijelaskan.

### 7.6 Too Good To Go — Referensi dari Domain Food Waste

Too Good To Go membingkai pengurangan sampah makanan sebagai aktivitas positif: menyelamatkan makanan, menghemat uang, dan memberi dampak.

**Pelajaran untuk Fresh:**

- narasi positif lebih menarik daripada rasa bersalah;
- dampak dapat ditampilkan sebagai celebration yang ringan;
- manfaat pribadi seperti hemat uang dan lebih tenang sama pentingnya dengan manfaat lingkungan.

---

## 8. Diferensiasi yang Disarankan

Fresh dapat mengambil posisi berikut:

> **A calm, visual food countdown that tells you what to use next.**

Artinya, Fresh bukan sekadar database dapur. Produk ini adalah lapisan keputusan yang membantu pengguna bertindak sebelum makanan terbuang.

Pilar pengalaman:

1. **See what matters now** — item diurutkan berdasarkan urgensi yang dapat dipahami.
2. **Act in one step** — gunakan, bekukan, pindahkan, atau bagikan.
3. **Add without effort** — input cepat dan belajar dari kebiasaan pengguna.
4. **Feel progress, not guilt** — tunjukkan makanan yang terselamatkan dan kebiasaan yang membaik.

---

## 9. Rancangan Awal Information Architecture

### Today

- ringkasan `Gunakan hari ini`;
- item yang mendekati batas;
- saran tindakan;
- progress ringan, misalnya makanan yang berhasil digunakan minggu ini.

### Inventory

- semua makanan;
- filter lokasi: fridge, freezer, pantry;
- pencarian, kategori, dan status;
- list sebagai tampilan utama, grid sebagai opsi jika foto memang konsisten.

### Add

- scan barcode;
- foto/label;
- quick add;
- recent item;
- manual entry sebagai fallback.

### Insights

- used vs discarded;
- kategori paling sering terbuang;
- estimasi uang atau item yang diselamatkan;
- rekomendasi kecil yang dapat dilakukan.

### Settings

- household dan sync;
- notification timing;
- unit, bahasa, dan format tanggal;
- accessibility dan privacy explanation.

Struktur final perlu menunggu keputusan scope MVP. `Insights` tidak harus menjadi tab utama pada versi pertama.

---

## 10. Rancangan Awal Design System

### 10.1 Foundations

- **Color:** primitive palette dan semantic roles untuk background, label, brand, status, separator, dan interactive state.
- **Typography:** San Francisco melalui SwiftUI Dynamic Type; style rounded hanya untuk countdown atau angka besar jika terbukti sesuai.
- **Spacing:** grid dasar 4 pt dengan ritme utama 8 pt.
- **Shape:** radius konsisten, misalnya 12 untuk control, 16 untuk card, dan 24 untuk hero container.
- **Iconography:** SF Symbols sebagai default; custom icon hanya ketika simbol sistem tidak cukup jelas.
- **Photography:** pencahayaan alami, background sederhana, temperatur warna konsisten, dan crop yang jelas.
- **Motion:** cepat, lembut, fungsional, serta memiliki alternatif Reduce Motion.

### 10.2 Semantic Tokens

Token sebaiknya menjelaskan fungsi, bukan rupa. Contoh:

- `background.canvas`
- `background.surface`
- `content.primary`
- `content.secondary`
- `action.primary`
- `status.fresh`
- `status.soon`
- `status.today`
- `status.expired`
- `border.subtle`

Dengan struktur ini, palette dapat berubah tanpa mengubah seluruh komponen.

### 10.3 Core Components

- Food Row
- Food Card
- Countdown Badge
- Status Label
- Primary / Secondary / Destructive Button
- Quick Date Picker
- Free-text Storage Field
- Search and Filter Bar
- Empty State
- Toast / Undo Banner
- Progress Summary
- Photo Placeholder

Setiap komponen perlu mendokumentasikan anatomy, variants, states, behavior, accessibility label, dan contoh penggunaan yang benar/salah.

### 10.4 Interaction Patterns

- quick add;
- edit food;
- consume all/partial;
- freeze or move storage;
- discard with reason;
- notification deep link;
- resolve expired item;
- undo destructive action;
- loading, empty, error, offline, dan sync conflict.

### 10.5 Content System

Tone of voice Fresh:

- singkat;
- konkret;
- hangat;
- tidak menghakimi;
- berorientasi tindakan;
- transparan ketika data hanyalah estimasi.

Contoh:

| Hindari | Gunakan |
|---|---|
| `Warning! Food expiring!` | `2 item sebaiknya digunakan hari ini` |
| `You wasted 5 items` | `5 item belum sempat digunakan` |
| `Bad food` | `Tanggalnya sudah lewat 2 hari` |
| `Save` | `Simpan makanan` atau `Simpan perubahan` |

---

## 11. Hal yang Sebaiknya Dihindari

- seluruh layar menggunakan hijau;
- hijau neon yang terasa seperti minuman energi;
- gradient berlebihan tanpa fungsi;
- glass/transparency di belakang informasi countdown yang menurunkan keterbacaan;
- foto stok bergaya iklan yang tidak mirip isi dapur nyata;
- gamification yang menimbulkan rasa bersalah;
- terlalu banyak statistik di beranda;
- status yang hanya dibedakan lewat warna;
- warna merah untuk semua hal yang mendekati tanggal;
- tipografi rounded pada seluruh body text;
- kartu di dalam kartu berlapis-lapis;
- mengejar “sehat” melalui klaim nutrisi yang tidak didukung data.

---

## 12. Hipotesis Pengalaman yang Perlu Divalidasi

1. Pengguna lebih membutuhkan daftar `use next` daripada inventaris lengkap.
2. Input harus selesai dalam hitungan detik agar penggunaan dapat bertahan.
3. Household sharing mungkin penting, tetapi dapat ditunda jika pengguna awal kebanyakan individu.
4. Foto membantu recognition, tetapi kewajiban memotret setiap item dapat menjadi friction.
5. Notifikasi bernilai hanya jika langsung membuka tindakan yang relevan.
6. Countdown relatif (`2 hari lagi`) lebih cepat dipahami daripada tanggal absolut, tetapi detail tetap perlu menunjukkan keduanya.
7. Pengguna Indonesia mungkin memerlukan preset makanan dan penyimpanan yang berbeda dari benchmark global.

---

## 13. Kesimpulan Arah Awal

Fondasi visual Fresh yang paling kuat adalah **calm organic utility**: antarmuka native iOS yang lapang dan mudah dipindai, diberi identitas botanical yang matang serta warna makanan sebagai aksen. Countdown menjadi elemen khas produk. Kejelasan harus mengambil prioritas di atas dekorasi, tetapi pengalaman tidak boleh terasa klinis.

Sebelum arah ini menjadi design specification final, kita perlu memutuskan target pengguna, scope MVP, serta karakter brand yang paling penting.

---

## Sumber Riset

- [Apple Human Interface Guidelines — Design principles](https://developer.apple.com/design/human-interface-guidelines/design-principles)
- [Apple Human Interface Guidelines — Color](https://developer.apple.com/design/human-interface-guidelines/color)
- [Apple Human Interface Guidelines — Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode)
- [Apple Human Interface Guidelines — Accessibility](https://developer.apple.com/design/human-interface-guidelines/accessibility/)
- [W3C — Web Content Accessibility Guidelines 2.2](https://www.w3.org/TR/WCAG22/)
- [PubMed — The Influence of Packaging Color on Consumer Perceptions of Healthfulness](https://pubmed.ncbi.nlm.nih.gov/37959030/)
- [FridgeBuddy — App Store](https://apps.apple.com/us/app/pantry-fridge-fridgebuddy/id1500190823)
- [NoWaste — Official website](https://www.nowasteapp.com/)
- [Pantry Check — App Store](https://apps.apple.com/us/app/pantry-check-grocery-list/id966702368)
- [FoodShiner — App Store](https://apps.apple.com/us/app/foodshiner-pantry-companion/id1507786821)
- [Yuka — App Store](https://apps.apple.com/us/app/yuka-food-cosmetic-scanner/id1092799236)
- [Too Good To Go — App Store](https://apps.apple.com/us/app/too-good-to-go-save-good-food/id1060683933)
