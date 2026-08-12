# Fresh: Food Countdown — App Concept & Feature Research

> Status: **draft untuk diskusi — belum disetujui**<br>
> Tanggal: 12 Agustus 2026<br>
> Platform awal: iOS / SwiftUI<br>
> Dokumen terkait: [UI/UX Design Research](./UI_UX_DESIGN_RESEARCH.md)

## 1. Ringkasan Konsep yang Sudah Dirapikan

**Fresh: Food Countdown** adalah aplikasi untuk orang yang suka memasak dan menyimpan bahan makanan di rumah. Pengguna mencatat bahan yang dibeli, kondisi bahan, dan cara penyimpanannya. Fresh lalu membantu memperkirakan kapan bahan tersebut sebaiknya digunakan, mengurutkan bahan berdasarkan urgensi, serta mengingatkan pengguna sebelum kualitasnya menurun.

Fresh bukan sekadar daftar isi kulkas. Nilai utamanya adalah menjawab satu pertanyaan sederhana:

> **Bahan mana yang sebaiknya aku gunakan lebih dulu?**

### Positioning statement

> Fresh membantu home cook mengingat bahan makanan yang mereka simpan dan menggunakan yang paling perlu lebih dulu, melalui countdown yang mudah dipahami dan rekomendasi penyimpanan yang transparan.

### Masalah yang diselesaikan

- bahan makanan terlupakan di kulkas, freezer, atau pantry;
- pengguna tidak tahu bahan mana yang perlu diprioritaskan;
- tanggal pembelian tidak selalu cukup untuk memperkirakan masa simpan;
- aplikasi inventaris makanan sering terasa terlalu rumit untuk dipakai setiap hari;
- kebingungan antara “kualitas mulai menurun” dan “sudah tidak aman dimakan” dapat menyebabkan pemborosan atau keputusan yang berisiko.

### Target pengguna awal

Asumsi sementara untuk dibahas:

- orang yang cukup sering memasak sendiri;
- menyimpan bahan mentah, makanan kemasan, atau sisa masakan di rumah;
- memakai iPhone;
- ingin mengurangi bahan terbuang tanpa harus mengelola inventaris yang kompleks.

---

## 2. Prinsip Produk

1. **Countdown first** — urutkan berdasarkan apa yang perlu digunakan lebih dulu.
2. **Fast to add** — mencatat bahan harus selesai dalam beberapa detik.
3. **Explain the estimate** — pengguna dapat melihat data dan asumsi di balik estimasi.
4. **AI assists, rules decide** — AI membantu memahami input; aturan berbasis sumber menjadi dasar estimasi.
5. **Quality is not the same as safety** — indikator kualitas tidak boleh disajikan sebagai diagnosis keamanan pangan.
6. **Calm, not alarming** — Fresh membantu pengguna bertindak tanpa mempermalukan atau menakut-nakuti.
7. **Useful without AI** — fungsi utama tetap berjalan ketika Apple Intelligence tidak tersedia.
8. **User stays in control** — pengguna dapat mengoreksi input, interpretasi kategori, tanggal, dan hasil estimasi sebelum menyimpan.

---

## 3. Rancangan Onboarding

Ide awal pengguna memiliki alur cerita yang bagus: kebiasaan memasak → kebiasaan menyimpan → masalah lupa → Fresh sebagai solusi. Agar onboarding tidak terlalu panjang, ceritanya sebaiknya diringkas menjadi tiga layar dan satu langkah interaktif.

Apple menyarankan onboarding yang cepat, menyenangkan, opsional, dan sebisa mungkin mengajarkan melalui interaksi. Pengaturan yang tidak penting serta permintaan izin sebaiknya ditunda sampai benar-benar dibutuhkan.

### Pendekatan A — Conversational Story, rekomendasi

Mempertahankan bentuk pertanyaan yang terasa personal, tetapi lebih singkat dari draft awal.

#### Layar 1 — Kebiasaan

**Judul**<br>
`Suka masak dan menyimpan bahan makanan di rumah?`

**Pendukung**<br>
`Punya stok membuat masak lebih praktis—selama kita masih ingat apa yang tersimpan.`

**Ilustrasi**<br>
Karakter sedang memasak, dikelilingi sayur, telur, dan bahan dapur dengan gaya cartoonish yang bersih.

#### Layar 2 — Masalah

**Judul**<br>
`Kadang ada yang terlupakan.`

**Pendukung**<br>
`Bahan yang terselip di kulkas bisa kehilangan kualitas sebelum sempat digunakan.`

**Ilustrasi**<br>
Bahan makanan bersembunyi di belakang isi kulkas; ekspresinya ringan, bukan menjijikkan atau menakutkan.

#### Layar 3 — Solusi

**Judul**<br>
`Gunakan yang paling perlu lebih dulu.`

**Pendukung**<br>
`Fresh mengatur bahan berdasarkan jenis, kondisi, dan cara penyimpanannya—lalu memberi countdown yang mudah dipahami.`

**CTA utama**<br>
`Tambahkan bahan pertama`

**CTA sekunder**<br>
`Lihat contoh dulu`

#### Langkah interaktif — First value

Alih-alih menambah slide keempat yang hanya menjelaskan fitur, pengguna langsung mencoba quick add dengan satu contoh bahan. Ini membuat mereka memahami fungsi Fresh melalui tindakan.

### Pendekatan B — Benefit First

Urutan layar:

1. `Tahu apa yang perlu digunakan hari ini.`
2. `Dapatkan countdown berdasarkan cara penyimpanan.`
3. `Kurangi bahan yang terlupakan.`

**Kelebihan:** sangat cepat menjelaskan manfaat.<br>
**Kekurangan:** kurang memiliki cerita dan personality.

### Pendekatan C — Interactive First

Setelah satu layar pembuka, pengguna langsung memilih satu contoh bahan dan melihat countdown demo.

**Kelebihan:** pengguna mengalami value proposition paling cepat.<br>
**Kekurangan:** lebih kompleks untuk dirancang dan dapat membingungkan sebelum mental model terbentuk.

### Rekomendasi onboarding

Gunakan **Pendekatan A**, tetapi akhiri dengan interaksi dari Pendekatan C. Totalnya tiga layar naratif, kemudian quick add. Sediakan `Lewati` sejak layar pertama. Jangan meminta izin notifikasi atau galeri sampai pengguna memakai fitur yang membutuhkannya.

---

## 4. Core Experience

### Core loop

1. Pengguna membeli atau menyiapkan makanan.
2. Pengguna menambah item ke Fresh.
3. Fresh mengenali jenis item dan mengambil panduan penyimpanan yang relevan.
4. Pengguna memeriksa dan mengonfirmasi estimasi.
5. Item muncul di daftar berdasarkan urgensi.
6. Fresh mengingatkan ketika item perlu segera digunakan.
7. Pengguna menandai item sebagai digunakan, dibekukan, dipindahkan, atau dibuang.
8. Item yang sering dibeli dapat ditambahkan kembali dengan cepat.

### North-star interaction

Beranda dibuka dan dalam beberapa detik pengguna bisa melihat:

- apa yang perlu digunakan hari ini;
- apa yang perlu digunakan dalam waktu dekat;
- apa yang masih memiliki cukup waktu;
- item mana yang membutuhkan pemeriksaan atau informasi tambahan.

---

## 5. Information Architecture Awal

### Tab 1 — Today

Halaman prioritas, bukan dashboard statistik.

- `Use Today`
- `Use Soon`
- rekomendasi singkat seperti `Bekukan ayam hari ini jika belum akan dimasak`
- ringkasan bahan yang berhasil digunakan minggu ini

### Tab 2 — My Food

Daftar seluruh bahan makanan.

- grouping berdasarkan urgency;
- filter fridge, freezer, pantry, dan room temperature;
- search;
- filter kategori;
- sort berdasarkan countdown, nama, atau terbaru ditambahkan.

### Add button

Tombol tambah menjadi aksi global yang mudah dijangkau. Ia tidak harus menjadi tab terpisah apabila sheet quick add sudah cukup jelas.

### Tab 3 — Activity atau Insights

Belum perlu menjadi tab MVP. Pada tahap selanjutnya dapat berisi:

- digunakan;
- dibuang;
- dibekukan;
- kategori yang paling sering tidak sempat digunakan;
- tren sederhana tanpa membuat pengguna merasa bersalah.

### Settings

- pengaturan notifikasi;
- unit dan format tanggal;
- data source dan penjelasan estimasi;
- privacy;
- tutorial ulang;
- Apple Intelligence availability;
- iCloud sync jika kelak didukung.

---

## 6. Bentuk Daftar Bahan Makanan

List adalah tampilan utama yang tepat karena pengguna perlu membandingkan banyak item dan urgency dengan cepat.

### Anatomy satu Food Row

1. ilustrasi atau foto bahan;
2. nama bahan;
3. lokasi penyimpanan;
4. countdown relatif, misalnya `2 hari lagi`;
5. status label dengan warna, teks, dan ikon;
6. satu quick action kontekstual bila diperlukan.

### Contoh

```text
[icon bayam]  Bayam
              Fridge · dibeli 2 hari lalu
              Use soon · sekitar 1 hari lagi
```

### Grouping yang disarankan

- `Use Today`
- `Use Soon`
- `Fresh`
- `Needs Review`

Urutan ini lebih action-oriented daripada hanya memisahkan daftar berdasarkan fridge, freezer, dan pantry. Lokasi tetap tersedia sebagai filter.

### Interaksi

- tap membuka detail;
- swipe satu arah untuk `Used`;
- swipe arah lain menampilkan menu `Freeze`, `Move`, atau `Discard`;
- tindakan destruktif menyediakan undo;
- jangan menaruh terlalu banyak tombol pada setiap row.

---

## 7. Sistem Ikon dan Foto Bahan

### Sumber visual item

Fresh mendukung tiga tingkat visual:

1. **Built-in food illustration** — pilihan utama untuk bahan umum.
2. **Category fallback illustration** — dipakai untuk bahan custom yang belum memiliki ikon khusus.
3. **User photo** — opsional dari kamera atau galeri.

### Mengapa bukan ikon kosong?

Ikon kosong terlihat seperti data gagal dimuat. Untuk item custom, fallback sebaiknya tetap memiliki ilustrasi generik berdasarkan kategori, misalnya vegetables, fruit, dairy, meat, seafood, grain, spice, beverage, cooked meal, atau other.

### Style ilustrasi

- cartoonish tetapi tidak childish;
- bentuk sederhana dan mudah dikenali pada ukuran kecil;
- outline lembut dengan fill warna makanan;
- pencahayaan dan perspektif konsisten;
- tidak memakai wajah pada setiap bahan agar layar tidak terlalu ramai;
- tetap terbaca dalam Light Mode dan Dark Mode;
- tidak bergantung pada warna saja untuk membedakan kategori.

### MVP icon library

Mulai dengan kumpulan yang kecil tetapi relevan untuk pengguna Indonesia, bukan ratusan ikon sekaligus. Kandidat awal:

- sayuran daun;
- cabai, tomat, bawang merah, bawang putih;
- kentang dan wortel;
- pisang, apel, jeruk;
- ayam, daging, ikan, udang;
- telur;
- susu, keju, yoghurt;
- nasi, mi, roti;
- tahu dan tempe;
- bumbu;
- sisa masakan;
- produk kemasan.

Daftar final memerlukan riset makanan yang paling sering disimpan oleh target pengguna.

### Foto pengguna

- user dapat crop ke rasio tetap;
- foto ditampilkan dalam container yang sama dengan ilustrasi;
- izin galeri diminta just-in-time;
- aplikasi harus tetap berfungsi penuh tanpa akses galeri;
- user dapat kembali ke ilustrasi default kapan saja.

---

## 8. Alur Menambah Bahan

### Prinsip

Input wajib harus sesedikit mungkin. User tidak wajib mengisi seluruh field untuk menyimpan item. Data tambahan ditampilkan melalui progressive disclosure, dan kekurangan informasi dikomunikasikan sebagai warning non-blocking.

### Input inti dari pengguna

Field berikut tetap boleh dikosongkan, tetapi kekurangannya dapat menurunkan confidence atau membuat estimasi belum tersedia:

| Field | Alasan |
|---|---|
| Nama bahan | Identitas item |
| Kondisi bahan | Teks bebas tentang kondisi relevan seperti mentah, matang, utuh, dipotong, dicuci, masih keras, atau sangat matang |
| Status kemasan | Teks bebas seperti masih tersegel, sudah dibuka, bocor, atau tidak berkemasan |
| Lokasi penyimpanan | Teks bebas seperti `rak atas kulkas`, `freezer`, atau `meja dapur` |
| Tanggal acuan | Tanggal beli, dimasak, dibuka, atau dipindahkan ke penyimpanan |

Tidak ada input kategori atau tingkat kematangan tersendiri. Tingkat kematangan, bila ingin dicatat, menjadi bagian dari teks `Kondisi bahan`, misalnya `alpukat masih keras`. Jika tidak disebutkan, Fresh menyimpannya sebagai tidak diketahui dan tidak menebaknya dari toko atau tempat pembelian.

### Interpretasi internal Fresh

Fresh mempertahankan teks asli pengguna, lalu mencoba membentuk nilai internal terbatas yang dibutuhkan rule engine:

| Teks pengguna | Contoh interpretasi internal |
|---|---|
| Nama `Bayam` | Kategori `sayuran berdaun` |
| Lokasi `rak atas kulkas` | Metode penyimpanan `refrigerator` |
| Kondisi `sudah dicuci dan dipotong` | Tag kondisi `washed`, `cut` |
| Kemasan `plastiknya masih rapat` | Status kemasan `sealed` |
| Kondisi `alpukat masih keras` | Tag kondisi `unripe` sebagai bagian kondisi, bukan field terpisah |

Kategori tidak diisi langsung dalam Quick Add. Fresh menghasilkan kandidat kategori melalui pencocokan katalog lokal dan, pada perangkat yang mendukung, Foundation Model. Hasilnya ditampilkan pada Estimate Review agar pengguna dapat mengoreksi interpretasi yang jelas salah. Foundation Model tidak boleh melengkapi kondisi, kemasan, kematangan, atau penyimpanan yang tidak dinyatakan pengguna.

### Field penting bila tersedia

- tanggal `Baik digunakan sebelum` dari kemasan;
- petunjuk penyimpanan pada kemasan;
- apakah pernah dibiarkan di luar pendingin;
- estimasi suhu kulkas atau freezer;
- jumlah dan satuan.

### Field opsional

- beli di mana;
- harga;
- catatan;
- ilustrasi atau foto;
- merek.

`Beli di mana` berguna untuk riwayat belanja atau re-add, tetapi tidak boleh dianggap sebagai faktor utama umur simpan. Kondisi, kemasan, suhu, dan cara penyimpanan jauh lebih relevan.

### Data completeness dan warning

Fresh membedakan dua tingkat kelengkapan informasi:

#### 1. Incomplete information

Muncul ketika masih ada field yang belum diisi, termasuk field opsional. Pesannya bersifat ringan dan tidak menghalangi penyimpanan.

Contoh:

> `Informasi belum lengkap`<br>
> `Kamu tetap bisa menyimpan bahan ini. Tambahkan detail lain agar catatanmu lebih lengkap.`

Fresh dapat menampilkan jumlah informasi yang belum diisi dan aksi `Lengkapi informasi`, tetapi tidak memaksa user mengisinya.

#### 2. Estimate may be less accurate

Muncul ketika informasi yang berpengaruh terhadap estimasi belum diketahui atau teksnya belum dapat dinormalisasi, misalnya kategori hasil pencocokan, kondisi, penyimpanan, tanggal acuan, atau status kemasan.

Contoh:

> `Perkiraan mungkin kurang akurat`<br>
> `Fresh belum mengetahui apakah ayam ini mentah atau sudah dimasak.`

Warning harus menyebutkan informasi yang hilang dan pengaruhnya, bukan hanya mengatakan bahwa form belum lengkap.

### Save behavior untuk data tidak lengkap

- user tetap dapat menekan `Save`;
- item disimpan dengan data yang tersedia;
- Foundation Model tidak boleh mengarang detail yang tidak diberikan;
- asumsi yang digunakan harus terlihat pada `Why this estimate?`;
- field yang tidak diketahui disimpan sebagai `unknown`, bukan nilai default yang terlihat pasti;
- jika estimasi belum dapat dibuat secara bertanggung jawab, item memakai status `Needs Review` dan copy `Tambahkan informasi untuk membuat perkiraan`;
- card dan halaman detail menampilkan indikator warning sampai informasi yang berpengaruh dilengkapi;
- setelah user melengkapi informasi dan menyimpan perubahan, klasifikasi serta estimasi dijalankan ulang.

Field opsional seperti toko, harga, merek, foto, dan catatan boleh memicu completeness hint, tetapi tidak menurunkan confidence estimasi kecuali benar-benar digunakan sebagai input.

### Quick-add flow yang disetujui

1. `Apa yang kamu simpan?`
2. Tulis nama bahan; foto opsional hanya untuk tampilan.
3. Tulis lokasi penyimpanan dengan bahasa sendiri, misalnya `rak atas kulkas`.
4. Tulis `Kondisi bahan` dan `Status kemasan` pada dua text field terpisah. Kematangan boleh disebut di kondisi, tetapi tidak ditanyakan sebagai field tersendiri.
5. Pilih jenis tanggal acuan dan isi tanggal bila diketahui.
6. Fresh mempertahankan teks asli, membuat interpretasi terstruktur tanpa mengarang detail, lalu rule engine mencari estimasi.
7. Fresh menampilkan kategori hasil interpretasi, nilai yang dipakai, sumber, confidence, dan asumsi.
8. User memilih `Simpan bahan` atau `Sesuaikan estimasi`.

Form lengkap tetap tersedia melalui `More details`.

---

## 9. Freshness Estimation: Tiga Pendekatan

### Pendekatan A — Foundation Model sebagai penentu utama

Model menerima nama bahan, lokasi beli, cara penyimpanan, dan tanggal, kemudian langsung menghasilkan jumlah hari serta status.

**Kelebihan:** cepat dibuat sebagai prototype dan terasa pintar.<br>
**Kekurangan:** output probabilistik, sulit direproduksi, dapat berhalusinasi, tidak cocok menjadi sumber fakta keamanan pangan, dan hanya tersedia pada device yang kompatibel.

**Keputusan:** tidak direkomendasikan untuk produksi.

### Pendekatan B — Rule/database only

Aplikasi memakai dataset terkurasi untuk memetakan jenis bahan, kondisi, cara penyimpanan, dan durasi. Semua hasil dihitung secara deterministik.

**Kelebihan:** dapat diuji, bekerja offline di semua device target, mudah menampilkan sumber, dan hasil konsisten.<br>
**Kekurangan:** pencarian nama bahan custom lebih kaku; dataset perlu dirawat dan dilokalkan.

**Keputusan:** aman sebagai fondasi, tetapi pengalaman input dapat terasa kurang fleksibel.

### Pendekatan C — Hybrid: Foundation Model + verified rules, rekomendasi

Foundation Model digunakan untuk:

- memahami nama custom seperti `sisa ayam kecap tadi malam`;
- mengekstrak kandidat kategori serta menormalkan teks lokasi, kondisi, kemasan, dan tanggal;
- memilih kandidat kategori dari database;
- mengajukan pertanyaan lanjutan yang relevan;
- menjelaskan estimasi dengan bahasa sederhana.

Foundation Model hanya boleh mengekstrak kematangan ketika pengguna sendiri menyatakannya di teks kondisi. Model tidak boleh menebak kematangan dari tempat membeli, merek, atau karakteristik rata-rata produk.

Rule engine dan database digunakan untuk:

- mengambil rentang penyimpanan dari sumber terkurasi;
- menghitung tanggal dan pergantian status;
- menerapkan tanggal kemasan;
- menangani aturan konservatif untuk kondisi berisiko;
- menghasilkan hasil yang dapat diuji dan direproduksi.

**Kelebihan:** input fleksibel tetapi keputusan tetap dapat diaudit; dapat memiliki fallback tanpa AI.<br>
**Kekurangan:** arsitektur serta pengujian lebih kompleks.

**Keputusan:** direkomendasikan.

### Mengapa Foundation Model tidak boleh menjadi database umur simpan?

Apple menjelaskan bahwa on-device Foundation Model cocok untuk summarization, extraction, dan classification, tetapi bukan untuk world knowledge atau advanced reasoning. Apple juga menyarankan agar AI tidak diminta menghasilkan fakta ketika kesalahan dapat menyesatkan atau membahayakan.

Foundation Models framework juga membutuhkan device kompatibel dengan Apple Intelligence dalam keadaan aktif. Karena itu, core countdown harus memiliki jalur non-AI.

### Proposed data flow

```text
Input user
    ↓
Preserve raw text
    ↓
Local matching + optional Foundation Model normalization
    ↓
User reviews category and ambiguous interpretations
    ↓
Verified storage guideline lookup
    ↓
Deterministic date calculation
    ↓
User reviews source + assumptions
    ↓
Countdown saved
```

### Structured output yang dibutuhkan

Foundation Model sebaiknya mengembalikan struktur terbatas, misalnya:

```text
foodNameRaw
matchedFoodCategory
storageTextRaw
storageMethod
conditionTextRaw
conditionTags
packageStatusTextRaw
packageStatus
referenceDateType
referenceDate
missingInformation
confidence
```

Model tidak langsung mengembalikan `safeToEat = true`.
Nilai hasil normalisasi harus dapat ditelusuri ke teks pengguna. Bila teks tidak menyebut suatu detail atau hasil tidak valid, field terstruktur tetap `unknown`.

---

## 10. Memperbaiki Sistem Tiga Label

Draft awal memakai:

- `Fresh` — hijau;
- `Not Fresh` — kuning;
- `Don't Eat` — merah.

Masalahnya, label tersebut mencampur **kualitas**, **urgensi**, dan **keamanan pangan**. Makanan yang melewati puncak kualitas belum tentu otomatis tidak aman, sementara makanan yang tampak dan berbau normal juga tidak selalu terbukti aman jika salah ditangani.

### Rekomendasi label utama

| Label | Warna | Arti UX | Contoh |
|---|---|---|---|
| Fresh | Hijau | Masih di bagian awal rentang panduan | `Sekitar 5 hari lagi` |
| Use Soon | Amber | Sudah mendekati akhir rentang panduan | `Sebaiknya gunakan dalam 2 hari` |
| Needs Review | Merah-tomat | Rentang panduan terlewati atau ada informasi penting yang perlu diperiksa | `Periksa sebelum digunakan` |

### Kapan boleh menampilkan `Do Not Eat`?

Hanya ketika ada dasar deterministik yang jelas, misalnya:

- tanggal kedaluwarsa pangan olahan sudah terlewati dan pedoman lokal menyatakan tidak boleh dikonsumsi;
- pengguna menyatakan makanan mudah rusak berada di luar suhu aman melebihi batas panduan;
- kemasan menggembung, bocor, atau menunjukkan kondisi bahaya yang didokumentasikan;
- aturan safety khusus yang bersumber dan telah divalidasi memang memerintahkan pembuangan.

Pesan ini harus menyertakan alasan singkat dan sumber. Jangan menghasilkan keputusan tersebut dari jawaban bebas Foundation Model.

### Status adalah estimasi, bukan sensor

Fresh tidak mengetahui suhu aktual, rantai dingin sebelum pembelian, kebersihan, kontaminasi silang, atau kondisi fisik makanan kecuali pengguna menginformasikannya. Karena itu:

- tampilkan `Estimated` atau `Perkiraan`;
- jelaskan asumsi;
- sediakan `Adjust estimate`;
- jangan memakai copy seperti `100% safe`;
- sediakan panduan tanda bahaya tanpa meminta pengguna mencicipi makanan untuk mengecek.

### Cara menghitung tiga fase

Banyak sumber menyediakan rentang penyimpanan, bukan pembagian ilmiah antara hari “fresh” dan “not fresh”. Oleh karena itu, perpindahan `Fresh → Use Soon` adalah indikator prioritas UX, bukan klaim laboratorium.

Proposal awal:

- `Fresh`: bagian awal sampai tengah rentang panduan;
- `Use Soon`: bagian akhir rentang panduan;
- `Needs Review`: rentang terlewati atau data tidak cukup;
- threshold berbeda menurut kategori dan dapat dikonfigurasi dalam dataset;
- jangan menggunakan persentase universal yang sama untuk semua jenis bahan tanpa validasi.

---

## 11. Detail Item

> **Status keputusan: disetujui pada 12 Agustus 2026.**

Ketika pengguna menekan sebuah Food Card atau Food Row, Fresh membuka halaman detail untuk item tersebut. Halaman ini harus membedakan dengan jelas informasi yang diberikan pengguna, hasil estimasi Fresh, dan informasi yang dibuat oleh Foundation Model.

### Header

- ilustrasi atau foto;
- nama;
- status `Fresh`, `Use Soon`, atau `Needs Review`;
- countdown besar, misalnya `Bertahan sekitar 3 hari lagi`;
- lokasi penyimpanan;
- tombol `Edit` yang selalu mudah ditemukan.

Countdown menggunakan kata `sekitar` atau penanda `Perkiraan` agar tidak terlihat seperti hasil sensor atau jaminan keamanan pangan.

### Freshness timeline

Timeline menampilkan:

- tanggal acuan;
- rentang Fresh;
- fase Use Soon;
- batas panduan;
- `today marker`.

Timeline perlu memakai teks dan ikon selain warna.

Contoh konseptual:

```text
Fresh ━━━━━●━━━━ Use Soon ━━━━━ Needs Review
           Hari ini
```

Di bawah timeline, tampilkan estimasi batas penyimpanan, tanggal mulai disimpan, kondisi saat ini, dan rekomendasi singkat seperti `Sebaiknya gunakan dalam 2–3 hari`.

### Informasi dari pengguna

Bagian ini hanya menampilkan field yang relevan dan telah diisi:

- nama bahan;
- jumlah dan satuan;
- kondisi bahan dalam teks asli, termasuk kematangan bila pengguna menyebutnya;
- status kemasan dalam teks asli;
- lokasi penyimpanan dalam teks asli;
- tanggal beli, dimasak, dibuka, atau mulai disimpan;
- tempat membeli;
- tanggal pada kemasan;
- merek dan catatan.

Informasi ini dapat diubah melalui tombol `Edit`.

Jika ada informasi yang belum diisi, bagian ini menampilkan banner ringan `Informasi belum lengkap` dan aksi `Lengkapi`. Jika yang hilang memengaruhi estimasi, gunakan warning yang lebih spesifik seperti `Perkiraan mungkin kurang akurat`.

### Why this estimate?

Bagian ini menjawab:

- kategori yang dipakai;
- kondisi yang berhasil ditafsirkan dari input;
- status kemasan yang berhasil ditafsirkan;
- metode penyimpanan hasil normalisasi;
- suhu asumsi;
- tanggal kemasan bila ada;
- sumber guideline;
- tingkat confidence.

Bagian ini menggunakan disclosure agar detail teknis tersedia tanpa memenuhi tampilan utama.

### About this food

Foundation Model dapat menghasilkan satu paragraf pendek mengenai karakter bahan dan cara penyimpanannya. Contoh:

> Bayam merupakan sayuran daun yang kualitasnya dapat menurun cukup cepat. Simpan dalam kondisi kering di dalam kulkas dan hindari mencucinya sebelum akan digunakan.

Aturannya:

- Foundation Model menyusun penjelasan dari fakta atau konteks terverifikasi yang diberikan aplikasi;
- model tidak digunakan sebagai sumber bebas untuk fakta keamanan pangan;
- teks harus spesifik terhadap kategori, kondisi, dan cara penyimpanan item;
- hindari klaim `aman`, `pasti basi`, diagnosis, atau jaminan;
- tampilkan disclosure kecil seperti `Generated with Apple Intelligence · Informational only`;
- jika Foundation Model tidak tersedia, tampilkan storage tip statis dari database atau sembunyikan bagian ini;
- user dapat mencoba membuat ulang teks jika hasilnya tidak berguna.

### Actions

- `Mark as used`
- `Freeze`
- `Move storage`
- `Edit details`
- `Discard`

Ketika item dipindahkan ke freezer atau dibuka, countdown dihitung ulang dari state transition tersebut dan riwayatnya disimpan.

### Edit and recompute flow

1. User menekan `Edit`.
2. Form dibuka dengan seluruh data sebelumnya.
3. User mengubah informasi lalu menekan `Save Changes`.
4. Fresh memvalidasi dan menyimpan input user.
5. Jika field yang memengaruhi estimasi berubah, Foundation Model melakukan pencocokan ulang.
6. Verified rule/database menghitung ulang countdown dan label.
7. Fresh memperbarui bagian `About this food` bila konteks yang relevan berubah.
8. User melihat hasil terbaru beserta sumber dan asumsi yang digunakan.

Interpreter dan estimator dijalankan ulang ketika nama, teks kondisi, tanggal acuan, teks status kemasan, atau teks lokasi penyimpanan berubah. Kategori dapat ikut berubah sebagai hasil interpretasi, tetapi bukan field input utama. Mengubah foto, tempat membeli, harga, atau catatan biasa tidak memicu recompute kecuali informasinya memang dipakai sebagai input estimasi.

Jika proses AI gagal, perubahan user tetap tersimpan. Estimasi terakhir tidak diganti diam-diam; tampilkan status `Needs update` dan aksi `Try Again`. Jika rule engine tetap dapat menghitung dari input terstruktur, gunakan hasil rule engine tanpa menunggu AI.

---

## 12. Edit dan Lifecycle Item

Item bukan hanya memiliki tanggal; ia memiliki perubahan kondisi.

### State transitions

- bought;
- opened;
- cut or prepared;
- cooked;
- moved to fridge;
- frozen;
- thawed;
- partially used;
- consumed;
- discarded.

Tidak semuanya perlu muncul di MVP, tetapi data model sebaiknya tidak menganggap item selalu statis.

### Edit behavior

- perubahan kondisi memicu estimasi baru;
- user melihat perbedaan sebelum menyimpan;
- manual override tidak ditimpa diam-diam oleh model;
- riwayat menyimpan alasan perubahan;
- kesalahan edit dapat di-undo.

---

## 13. Notifikasi

Notifikasi sebaiknya berbasis tindakan, bukan sekadar alarm.

### Contoh

- `Bayam sebaiknya digunakan hari ini.`
- `Ayam akan masuk Use Soon besok. Bekukan jika belum akan dimasak.`
- `Tanggal pada yoghurt perlu diperiksa hari ini.`

### Aturan

- minta izin setelah user menyimpan item pertama atau mengaktifkan reminder;
- batasi bundling agar sepuluh bahan tidak menghasilkan sepuluh notifikasi;
- deep link langsung ke item atau daftar terkait;
- user dapat memilih waktu reminder;
- jangan mengirim peringatan safety yang tidak didukung data.

---

## 14. Fitur Tambahan untuk Dibahas

Semua fitur di bagian ini masih **proposal, bukan scope yang disetujui**.

### Kandidat MVP

| Fitur | Rekomendasi | Alasan |
|---|---|---|
| Onboarding 3 layar + skip | Masuk MVP | Menjelaskan value proposition |
| Add manual + suggested items | Masuk MVP | Jalur input paling dapat diandalkan |
| Built-in illustrations + category fallback | Masuk MVP | Recognition tanpa mewajibkan foto |
| User photo dari galeri | Masuk MVP jika waktu cukup | Personalisasi, tetapi bukan core |
| Free-text storage, condition, and package input | Masuk MVP | Raw text disimpan dan dinormalisasi bila memungkinkan |
| Verified rule/database | Masuk MVP | Fondasi countdown |
| List grouped by urgency | Masuk MVP | Pengalaman utama |
| Detail + edit + mark used/discarded | Masuk MVP | Menyelesaikan lifecycle |
| Local notifications | Masuk MVP | Membantu sebelum terlambat |
| Explain estimate | Masuk MVP | Trust dan safety |
| Foundation Model matching | Eksperimental/MVP+ | Harus memiliki fallback |

### Phase 2

- scan label tanggal dengan Vision/OCR;
- barcode lookup;
- re-add recent/frequent items;
- Home Screen widget `Use Today`;
- Spotlight/App Intents untuk quick add;
- freeze recommendation;
- riwayat item dan waste insight;
- iCloud sync;
- household sharing;
- kamera sebagai alternatif galeri.

### Later / perlu validasi kuat

- saran resep dari bahan yang mendekati batas;
- rekomendasi belanja berdasarkan stok;
- price tracking dan estimasi uang terselamatkan;
- automatic recognition dari foto kulkas;
- crowdsourced shelf-life data;
- integrasi suhu kulkas pintar;
- gamification dan achievements;
- health/nutrition scoring.

### Yang sebaiknya tidak masuk versi pertama

- marketplace;
- social feed;
- meal planner lengkap;
- calorie tracker;
- nutrition diagnosis;
- AI chat umum;
- household roles yang kompleks;
- cloud account wajib.

---

## 15. Empty, Loading, Error, dan AI-unavailable States

### Empty inventory

**Copy**<br>
`Belum ada bahan di Fresh.`<br>
`Tambahkan satu bahan untuk melihat apa yang perlu digunakan lebih dulu.`

**CTA**<br>
`Tambahkan bahan`

### Tidak menemukan kategori

- jangan mengarang hasil;
- tampilkan kategori sebagai interpretasi Fresh, bukan field Quick Add;
- tampilkan beberapa kandidat hanya saat perlu mengoreksi interpretasi;
- izinkan user memilih kategori umum melalui tindakan koreksi di Estimate Review;
- izinkan manual estimate;
- tandai confidence rendah.

### Informasi belum cukup

Ajukan satu pertanyaan paling berdampak, misalnya:

`Ayam ini masih mentah atau sudah dimasak?`

Jangan meminta semua kemungkinan detail sekaligus.

### Foundation Model tidak tersedia

- pertahankan seluruh input teks bebas pengguna;
- gunakan pencocokan katalog/alias lokal dan form normal;
- rule engine tetap menghitung;
- jangan memblokir add flow;
- jelaskan bahwa smart interpretation tidak tersedia, bukan bahwa Fresh tidak dapat digunakan.

### Guideline tidak tersedia

- user dapat memasukkan tanggal sendiri;
- status menjadi `Custom estimate`;
- jangan memberikan label safety otomatis;
- data dapat dianonimkan untuk riset hanya dengan persetujuan eksplisit.

---

## 16. Privacy dan Trust

- simpan data lokal secara default;
- Foundation Models on-device dapat membantu menjaga input tetap di perangkat pada device yang mendukung;
- jelaskan kapan AI digunakan;
- bedakan hasil AI, hasil rule, tanggal dari kemasan, dan tanggal manual;
- foto tidak perlu diunggah ke server untuk MVP;
- jangan memakai data lokasi toko untuk iklan;
- berikan delete/export data yang jelas pada tahap lanjutan;
- dokumentasikan versi dataset agar perubahan estimasi dapat dilacak.

---

## 17. Pengujian yang Dibutuhkan Kelak

### Usability

- apakah first-time user memahami arti tiga status;
- apakah user dapat menambah bahan dalam waktu singkat;
- apakah `Needs Review` dipahami sebagai permintaan pemeriksaan, bukan vonis;
- apakah user menemukan sumber estimasi;
- apakah swipe actions dapat ditemukan tanpa tutorial panjang.

### Rule engine

- kombinasi kategori × kondisi × storage;
- normalisasi teks lokasi, kondisi, dan kemasan tanpa kehilangan raw text;
- kematangan hanya diekstrak dari kondisi ketika disebutkan dan tetap unknown jika tidak disebutkan;
- boundary tanggal dan zona waktu;
- opened vs unopened;
- freeze/thaw transition;
- expired label precedence;
- manual override;
- missing data dan conflict.

### Foundation Model

- evaluasi dataset prompt berbahasa Indonesia;
- makanan lokal dan istilah informal;
- ambiguous input;
- structured output validity;
- tool-call correctness;
- hallucination and refusal behavior;
- fallback saat model tidak tersedia.

### Accessibility

- VoiceOver;
- Dynamic Type ukuran terbesar;
- color blindness;
- Reduce Motion;
- Increase Contrast;
- Light dan Dark Mode.

---

## 18. Rekomendasi Scope MVP

### MVP yang paling fokus

Fresh versi pertama cukup membuktikan satu loop:

> **Add → Estimate → Prioritize → Remind → Resolve**

Isi MVP:

1. onboarding ringkas;
2. suggested ingredient illustrations dan fallback kategori;
3. quick add + form detail;
4. rule-based storage guideline;
5. list grouped by urgency;
6. detail dan explain estimate;
7. edit;
8. mark used, freeze/move, atau discard;
9. local notification;
10. Foundation Model hanya sebagai enhancement dengan fallback.

Fitur recipe, household sharing, shopping list, barcode, OCR, dan insight dapat menunggu sampai core loop terbukti berguna.

---

## 19. Bagian yang Membutuhkan Approval

Dokumen ini belum mengunci keputusan berikut:

1. onboarding memakai Conversational Story tiga layar;
2. target awal adalah home cook yang menyimpan bahan dan leftovers;
3. list dikelompokkan berdasarkan urgency, bukan storage;
4. built-in illustration menjadi default, foto user bersifat opsional;
5. label utama menjadi `Fresh`, `Use Soon`, dan `Needs Review`;
6. `Do Not Eat` hanya muncul dari aturan yang tervalidasi, bukan tebakan AI;
7. sistem memakai hybrid Foundation Model + verified rule database;
8. MVP dibatasi pada loop Add → Estimate → Prioritize → Remind → Resolve;
9. fitur tambahan mengikuti prioritas pada Bagian 14.

Approval sebaiknya dilakukan per bagian agar keputusan mudah direvisi.

### Keputusan yang sudah disetujui

- Struktur halaman Detail Item pada Bagian 11: hero, freshness condition, informasi user, `Why this estimate?`, AI-generated `About this food`, actions, serta edit-and-recompute flow.
- User boleh menyimpan item tanpa mengisi seluruh field. Fresh menampilkan warning kelengkapan non-blocking, dan warning yang lebih kuat bila informasi yang hilang memengaruhi estimasi.

---

## 20. Sumber Riset

### Product dan AI design

- [Apple Human Interface Guidelines — Onboarding](https://developer.apple.com/design/human-interface-guidelines/onboarding)
- [Apple Human Interface Guidelines — Launching](https://developer.apple.com/design/human-interface-guidelines/launching/)
- [Apple Human Interface Guidelines — Generative AI](https://developer.apple.com/design/human-interface-guidelines/generative-ai)
- [Apple Developer — Meet the Foundation Models framework](https://developer.apple.com/videos/play/wwdc2025/286/)
- [Apple Developer Documentation — LanguageModelSession](https://developer.apple.com/documentation/FoundationModels/LanguageModelSession)

### Food storage dan safety

- [BPOM — Kenali Penandaan Kedaluwarsa Pada Produk Pangan Olahan](https://www.pom.go.id/katabpom/kenali-penandaan-kedaluwarsa-pada-produk-pangan-olahan)
- [BPOM — Contoh Label Pangan Olahan](https://rumahsiripo.pom.go.id/peraturan/label/contoh-label-pangan-olahan/)
- [WHO — Five Keys to Safer Food](https://www.who.int/activities/promoting-safe-food-handling/five-key-to-safer-food/)
- [FoodSafety.gov — FoodKeeper App](https://www.foodsafety.gov/keep-food-safe/foodkeeper-app)
- [FoodSafety.gov — Cold Food Storage Chart](https://www.foodsafety.gov/food-safety-charts/cold-food-storage-charts)
- [FDA — How to Cut Food Waste and Maintain Food Safety](https://www.fda.gov/food/consumers/how-cut-food-waste-and-maintain-food-safety)
- [USDA FSIS — Food Product Dating](https://www.fsis.usda.gov/food-safety/safe-food-handling-and-preparation/food-safety-basics/food-product-dating)
