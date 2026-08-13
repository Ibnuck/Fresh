# Fresh Agentic Development Design

> Status: disetujui pengguna pada 12 Agustus 2026; fondasi dokumentasi sedang diterapkan sebelum implementation planning.

## 1. Tujuan

Menyiapkan proyek pribadi Fresh agar dapat dikembangkan dengan workflow agentic yang konsisten, mudah diperiksa, dan tidak berlebihan. Setup harus membantu Codex memahami proyek, merencanakan mini-feature, menulis serta menguji kode Swift, kemudian memakai reviewer subagent baru untuk menilai setiap hasil secara independen.

Desain ini juga menetapkan arsitektur awal aplikasi dan format dokumentasi halaman yang cukup eksplisit untuk dibaca oleh manusia, coding agent, dan image-generation agent eksternal.

## 2. Kondisi Proyek Saat Ini

- Proyek merupakan starter app SwiftUI bernama Fresh.
- Target saat ini adalah iOS 26.5 dan Swift 5.0 berdasarkan konfigurasi Xcode.
- UI masih berupa `Hello, world!`.
- Test target memakai Swift Testing dan UI test target memakai XCTest.
- Riset produk berada di `Fresh/Docs/APP_CONCEPT_RESEARCH.md`.
- Riset visual berada di `Fresh/Docs/UI_UX_DESIGN_RESEARCH.md`.
- Git baru diinisialisasi sebagai bagian dari setup ini.

## 3. Keputusan Desain

### 3.1 Pendekatan yang dipilih

Gunakan **Lightweight Agentic Loop**: satu agent utama, satu custom reviewer read-only, satu skill workflow per proyek, dokumentasi spec/plan/review, serta build dan test sebagai sumber kebenaran.

Pendekatan ini dipilih karena menyediakan disiplin spec-driven dan review independen tanpa kompleksitas orchestrator multi-agent, banyak role, hooks, MCP, atau plugin kustom.

### 3.2 Pendekatan yang tidak dipilih

- Setup minimal yang hanya berisi `AGENTS.md` tidak menyediakan reviewer independen dan workflow reusable yang diminta.
- Framework penuh dengan banyak agent, Spec Kit lengkap, hooks, MCP, dan plugin terlalu berat untuk proyek pribadi pada tahap ini.
- Plugin dan MCP tidak dipasang di awal. Tambahkan hanya jika muncul kebutuhan konkret seperti GitHub PR, Figma, atau data eksternal yang sering berubah.

## 4. Arsitektur File Agentic

```text
Fresh/
├── AGENTS.md
├── README.md
├── .gitignore
├── .codex/
│   ├── config.toml
│   └── agents/
│       └── reviewer.toml
├── .agents/
│   └── skills/
│       ├── fresh-code-review/
│       ├── fresh-git-workflow/
│       ├── swiftui-pro/
│       ├── swiftdata-pro/
│       ├── swift-concurrency-pro/
│       └── swift-testing-pro/
├── docs/
│   └── superpowers/
│       ├── specs/
│       └── plans/
├── docs/
│   └── Development/
│       ├── WORKFLOW.md
│       ├── ARCHITECTURE.md
│       ├── PRODUCT_ROADMAP.md
│       └── Reviews/
└── Fresh/
    └── Docs/
        ├── APP_CONCEPT_RESEARCH.md
        ├── UI_UX_DESIGN_RESEARCH.md
        ├── DESIGN_SYSTEM.md
        ├── VISUAL_GENERATION_GUIDE.md
        ├── SCREEN_SPEC_TEMPLATE.md
        ├── ScreenSpecs/
        └── VisualReferences/
```

### Tanggung jawab file

- `AGENTS.md`: petunjuk permanen yang otomatis dibaca coding agent, termasuk struktur repo, perintah build/test, batas scope, dan definition of done.
- `.codex/config.toml`: konfigurasi Codex khusus repo dan batas concurrency yang konservatif.
- `.codex/agents/reviewer.toml`: agent sempit, read-only, yang hanya menemukan masalah berbukti dan tidak memperbaiki kode.
- `.agents/skills/fresh-code-review/SKILL.md`: quality gate read-only untuk QA/QC, correctness, accessibility, safety wording, persistence, dan test gaps.
- `.agents/skills/fresh-git-workflow/SKILL.md`: quality gate untuk branch, commit, remote, push, dan draft PR khusus repo Fresh.
- `swiftui-pro`, `swiftdata-pro`, `swift-concurrency-pro`, dan `swift-testing-pro`: referensi Swift terpilih dari katalog Paul Hudson. Toolchain aktual proyek tetap lebih berwenang daripada target versi yang tertulis di skill.
- `docs/superpowers/specs/`: keputusan desain sebelum implementasi.
- `docs/superpowers/plans/`: rencana implementasi terperinci.
- `docs/Development/Reviews/`: hasil review yang perlu disimpan sebagai artefak proyek.
- `Fresh/Docs/ScreenSpecs/`: satu visual specification untuk setiap halaman aplikasi.
- `Fresh/Docs/VisualReferences/`: proposal visual eksternal; bukan sumber kebenaran sampai disetujui.

## 5. Feature Development Loop

Setiap pekerjaan dibagi menjadi goal/mini-feature yang memiliki hasil dapat diuji. Setiap plan dan laporan penyelesaian wajib menuliskan **Ringkasan hasil**: satu sampai tiga kalimat yang menjelaskan kemampuan nyata yang diperoleh pengguna setelah goal selesai.

| Goal | Branch feature | Ringkasan hasil yang harus dicapai | Selesai ketika |
|---|---|---|---|
| G00 Agentic Foundation | `feature/g00-agentic-foundation` | Percakapan coding baru dapat memahami proyek, menjalankan workflow konsisten, dan meminta reviewer fresh tanpa konteks lama. | Instruksi, skills, Git workflow, review protocol, visual handoff, dan `.gitignore` tervalidasi. Fondasi awal boleh langsung masuk `main`. |
| G01 App Shell | `feature/g01-app-shell` | Fresh dapat dibuka sebagai aplikasi SwiftUI native dengan root navigation dan dependency container yang stabil. | App build, launch, navigasi dasar bekerja, dan smoke test lulus. |
| G02 Freshness Domain | `feature/g02-freshness-domain` | Aplikasi dapat menghitung status `Use Today`, `Use Soon`, `Fresh`, atau `Needs Review` secara deterministik dan dapat dijelaskan. | Boundary, timezone, missing/conflicting data, dan override memiliki unit test. |
| G03 Onboarding | `feature/g03-onboarding` | Pengguna baru memahami manfaat Fresh, dapat skip, dan dapat menuju penambahan bahan pertama. | Tiga langkah, persistence status onboarding, accessibility, dan UI flow test selesai. |
| G04 Core Empty States | `feature/g04-core-empty-states` | Pengguna dapat berpindah antara Today dan My Food serta memahami apa yang harus dilakukan saat belum ada data. | Navigation, empty states, CTA Add, Dynamic Type, dan VoiceOver diperiksa. |
| G05 Add and Estimate | `feature/g05-add-and-estimate` | Pengguna dapat menambah bahan dengan data minimal, melihat asumsi estimasi, lalu menyimpan atau menyesuaikannya. | Draft tidak hilang, unknown tidak dipalsukan, persistence error terlihat, dan flow test lulus. |
| G06 Live Inventory | `feature/g06-live-inventory` | Today dan My Food menampilkan data nyata yang otomatis dikelompokkan berdasarkan urgensi. | Save/update tercermin di kedua halaman; search, filter storage, empty/error state diuji. |
| G07 Food Lifecycle | `feature/g07-food-lifecycle` | Pengguna dapat melihat alasan estimasi dan menandai bahan Used, Frozen, Moved, Edited, atau Discarded. | Setiap action memperbarui data/status secara benar dan memiliki regression coverage. |
| G08 Reminders and Settings | `feature/g08-reminders-settings` | Pengguna mengendalikan reminder, format tanggal, privacy, onboarding, dan fitur intelligence. | Permission denied, scheduling failure, setting persistence, dan notification boundary ditangani. |
| G09 Optional Intelligence | `feature/g09-optional-intelligence` | Jika tersedia, AI on-device membantu interpretasi input tanpa menjadi sumber fakta atau syarat aplikasi berfungsi. | Fallback non-AI tetap penuh; invalid output dan unavailable state diuji. |
| G10 Release Quality | `feature/g10-release-quality` | MVP memiliki kualitas aksesibilitas, visual, regression, dan dokumentasi yang layak dipakai pribadi. | Full test suite, simulator matrix yang disepakati, visual QA, dan fresh reviewer final bersih. |

Setiap mini-feature mengikuti loop berikut:

```text
Research
  → Feature spec
  → Implementation plan dan acceptance criteria
  → Failing test bila behavior dapat diuji
  → Minimal implementation
  → Relevant tests
  → Full build/test verification
  → Fresh read-only reviewer subagent
  → Perbaikan bila ada temuan valid
  → Reviewer subagent baru
  → Selesai ketika verification dan review bersih
```

### Definition of done mini-feature

Mini-feature selesai hanya jika:

- acceptance criteria dalam spec terpenuhi;
- tidak ada placeholder `TODO` pada jalur behavior yang diklaim selesai;
- relevant tests lulus;
- full build dan test suite yang berlaku lulus;
- error, empty, dan unavailable state yang relevan ditangani;
- accessibility yang relevan diperiksa;
- reviewer baru tidak menemukan masalah correctness, regression, safety, atau missing-test berprioritas tinggi;
- dokumentasi dan keputusan yang berubah diperbarui.

### Ringkasan penyelesaian wajib

Saat sebuah goal ditutup, agent utama memberikan ringkasan dengan format:

```markdown
## Gxx — Nama goal

Ringkasan hasil: kemampuan pengguna yang sekarang benar-benar tersedia.

- Yang berubah: file/fitur utama.
- Verifikasi: build/test/inspection yang dijalankan dan hasilnya.
- Review fresh: jumlah siklus dan hasil terakhir.
- Risiko tersisa: hanya risiko nyata atau `Tidak ada yang diketahui`.
- Branch/commit: nama branch dan hash/pesan commit.
```

## 6. Fresh Reviewer Protocol

### 6.1 Sifat reviewer

- Setiap review memakai subagent baru dengan konteks percakapan bersih.
- Reviewer menggunakan sandbox read-only.
- Reviewer tidak mengedit file, membuat commit, atau menilai berdasarkan hubungan dengan agent utama.
- Reviewer berfokus pada correctness, regresi, food-safety wording, privacy, accessibility, dan test gaps.
- Komentar style-only tidak dilaporkan kecuali menyembunyikan risiko nyata.

### 6.2 Review packet

Agent utama memberikan konteks minimal yang cukup:

- tujuan mini-feature;
- feature spec dan acceptance criteria;
- implementation plan yang berlaku;
- diff atau daftar file yang berubah;
- hasil build dan test terbaru;
- area yang secara eksplisit berada di luar scope.

Reviewer tetap bebas membaca kode terkait untuk menelusuri execution path. Ia tidak menerima histori diskusi atau opini reviewer sebelumnya.

### 6.3 Format temuan

Setiap temuan harus memuat:

- prioritas `P0` hingga `P3`;
- lokasi file dan simbol/baris;
- behavior yang salah atau risiko konkret;
- bukti atau langkah reproduksi;
- alasan mengapa acceptance criteria atau prinsip proyek dilanggar;
- test yang hilang bila relevan.

Reviewer mengembalikan `No material findings` bila tidak menemukan masalah material. Reviewer tidak wajib menciptakan kritik agar terlihat berguna.

### 6.4 Repair and re-review loop

1. Agent utama memverifikasi setiap temuan secara teknis.
2. Temuan valid diperbaiki dan mendapatkan regression test jika sesuai.
3. Build serta test dijalankan ulang.
4. Reviewer lama dianggap selesai.
5. Reviewer baru dibuat menggunakan review packet terbaru.
6. Loop berulang sampai tidak ada temuan material.

Jika masalah akar yang sama bertahan setelah tiga siklus perbaikan, agent utama berhenti melakukan patch tambahan, menjalankan analisis akar masalah, dan meminta keputusan pengguna bila perubahan arsitektur atau scope diperlukan. Batas ini mencegah loop tanpa akhir tanpa menurunkan standar kualitas.

## 7. Arsitektur Aplikasi SwiftUI

Gunakan arsitektur feature-first yang ringan:

```text
SwiftUI View
  → user action
@Observable Feature Model
  → Service atau Repository
  → SwiftData dan bundled freshness rules
```

Tidak diperlukan Clean Architecture dengan banyak lapisan abstraksi. Setiap unit harus memiliki satu tanggung jawab dan interface yang dapat diuji.

```text
Fresh/
├── App/
│   ├── FreshApp.swift
│   ├── AppRootView.swift
│   └── AppDependencies.swift
├── Features/
│   ├── Onboarding/
│   ├── Today/
│   ├── Inventory/
│   ├── FoodEditor/
│   ├── FoodDetail/
│   └── Settings/
├── Core/
│   ├── Models/
│   ├── Persistence/
│   ├── Freshness/
│   ├── Notifications/
│   └── Intelligence/
├── DesignSystem/
│   ├── Components/
│   ├── Styles/
│   └── Assets/
├── Resources/
│   └── FreshnessRules/
└── Docs/
```

### Dependency rules

- `Features` boleh memakai `Core` dan `DesignSystem`.
- `Core` tidak boleh mengimpor `Features`.
- `DesignSystem` tidak mengetahui business rules.
- View tidak menghitung freshness secara langsung.
- Foundation Models tidak menjadi sumber fakta umur simpan atau keputusan keamanan pangan.
- Protocol dibuat hanya pada boundary yang benar-benar perlu ditukar atau dipalsukan dalam test.

## 8. Navigasi dan Halaman MVP

Navigasi utama hanya memiliki `Today`, `My Food`, tombol global `Add`, serta akses `Settings` dari toolbar. `Insights`, recipe, household sharing, barcode, OCR, dan shopping list tidak masuk MVP.

### 8.1 Onboarding

Tiga layar: kebiasaan memasak, bahan yang terlupakan, lalu manfaat Fresh. Pengguna dapat melewati onboarding. CTA terakhir adalah `Tambahkan bahan pertama` dan membuka Quick Add.

### 8.2 Today

Halaman tindakan yang memperlihatkan `Use Today`, `Use Soon`, saran singkat yang dapat dilakukan, empty state, dan tombol tambah. Halaman ini tidak menjadi dashboard statistik.

### 8.3 My Food

Seluruh bahan dikelompokkan menurut `Use Today`, `Use Soon`, `Fresh`, dan `Needs Review`. Tersedia search serta filter storage. Urgency menjadi pengelompokan utama; storage menjadi filter.

### 8.4 Quick Add

Satu sheet scrollable menampilkan nama wajib, foto opsional/dekoratif, lokasi penyimpanan sebagai text field, kondisi makanan dan status kemasan sebagai dua text field, pilihan tanggal acuan, serta `Detail lainnya` yang collapsed. CTA `Tinjau estimasi` membuka Estimate Review tanpa menyimpan. Quick Add bukan wizard bertahap.

Kategori dan tingkat kematangan bukan field input. Kategori dihasilkan melalui pencocokan lokal dan optional Foundation Model; kematangan hanya ditafsirkan bila pengguna menyebutkannya di teks kondisi. Teks asli disimpan bersama nilai normalisasi. Data tambahan berada di `More Details`. Informasi tidak lengkap tidak memblokir penyimpanan. Nilai yang belum diketahui disimpan sebagai `unknown`, bukan default palsu.

### 8.5 Estimate Review

Menampilkan countdown, kategori hasil interpretasi, teks pengguna serta normalisasinya, asumsi, confidence, sumber rule, dan pilihan `Simpan bahan` atau `Sesuaikan estimasi`. Jika estimasi bertanggung jawab belum dapat dibuat, gunakan `Needs Review` dan minta satu informasi paling berdampak tanpa membuat field kematangan tersendiri.

### 8.6 Food Detail

Menampilkan foto/ilustrasi, countdown besar, freshness timeline, data pengguna, `Why this estimate?`, storage tip, serta tindakan `Used`, `Freeze`, `Move`, `Edit`, dan `Discard`.

### 8.7 Edit Food

Menggunakan form yang sama dengan Quick Add. Perubahan nama, teks kondisi, teks storage, teks status kemasan, atau tanggal menghitung ulang interpretasi dan estimasi. Kategori dapat berubah sebagai hasil interpretasi, bukan sebagai field utama. Perubahan foto, toko, harga, atau catatan tidak memicu recompute kecuali kelak menjadi input eksplisit.

### 8.8 Settings

Hanya memuat notifikasi, format tanggal, privacy, sumber freshness rules, reset onboarding, dan status Apple Intelligence.

## 9. Data Flow

```text
FoodDraft
  → preserve raw user text
  → local matching + optional on-device AI normalization
  → user confirms ambiguous fields
  → deterministic FreshnessEngine
  → FoodItem saved to SwiftData
  → notification scheduled
  → Today and My Food update from persisted data
```

### AI unavailable

- Form, suggestions, rule engine, dan save tetap berfungsi.
- Smart interpretation disembunyikan atau ditandai tidak tersedia.
- Kegagalan AI tidak menghapus input pengguna.
- Jika structured input cukup, rule engine tetap menghitung tanpa AI.

### Guideline unavailable

- Pengguna dapat memasukkan estimasi manual.
- Status diberi label `Custom estimate` atau `Needs Review` sesuai kelengkapan.
- Aplikasi tidak menghasilkan label safety otomatis.

### Persistence atau notification error

- Kegagalan save ditampilkan dan draft dipertahankan untuk retry.
- Kegagalan notification tidak membatalkan item yang sudah berhasil disimpan.
- Settings menjelaskan bila izin notification ditolak.

## 10. Testing Strategy

### Unit tests

- freshness status boundaries dan zona waktu;
- kategori × normalized condition × normalized storage;
- raw-text preservation dan fallback normalisasi storage/condition/package;
- kematangan hanya berasal dari teks kondisi yang dinyatakan pengguna;
- opened, frozen, thawed, dan manual override;
- precedence label package dan rule;
- missing data dan conflicting data;
- feature model state transitions;
- AI fallback dan invalid structured output.

### Integration tests

- SwiftData save, fetch, update, dan delete;
- recompute ketika field estimasi berubah;
- notification scheduling boundary;
- migration bila data model berubah.

### UI tests

- onboarding dapat dilewati;
- item pertama dapat ditambahkan;
- incomplete data tetap dapat disimpan;
- item tampil dalam urgency group yang benar;
- edit memicu recompute;
- lifecycle action memperbarui atau menghilangkan item.

### Accessibility and visual verification

- VoiceOver labels memuat nama, status, storage, dan action;
- Dynamic Type terbesar tidak memotong informasi penting;
- status tidak dibedakan melalui warna saja;
- Light Mode, Dark Mode, Increase Contrast, dan Reduce Motion diperiksa;
- screenshot atau simulator inspection digunakan untuk halaman visual penting.

## 11. Visual Documentation for Image Generation

Dokumentasi UI harus dapat berfungsi sebagai prompt visual terstruktur. Sumber kebenaran terdiri dari:

```text
Fresh/Docs/
├── DESIGN_SYSTEM.md
├── VISUAL_GENERATION_GUIDE.md
├── SCREEN_SPEC_TEMPLATE.md
├── ScreenSpecs/
│   ├── 01_ONBOARDING.md
│   ├── 02_TODAY.md
│   ├── 03_MY_FOOD.md
│   ├── 04_QUICK_ADD.md
│   ├── 05_ESTIMATE_REVIEW.md
│   ├── 06_FOOD_DETAIL.md
│   ├── 07_EDIT_FOOD.md
│   └── 08_SETTINGS.md
└── VisualReferences/
    └── GENERATED_UI_PROPOSAL.md
```

### Required screen-spec sections

Setiap screen spec wajib memuat:

1. YAML metadata: screen ID, nama, platform, target OS, device frame, appearance, state, dan approval status.
2. Tujuan halaman dalam satu kalimat.
3. Primary user action.
4. Hierarki visual bernomor.
5. Layout dari atas ke bawah dengan posisi, spacing, alignment, dan behavior.
6. Copy UI persis.
7. Daftar komponen beserta nama SwiftUI yang direncanakan.
8. Data contoh yang konsisten lintas halaman.
9. Arah visual dan design tokens.
10. State: populated, empty, loading, error, large Dynamic Type, dan Dark Mode bila berlaku.
11. Accessibility requirements.
12. Hal yang dilarang.
13. Output image yang diminta.

### Canonical metadata

```yaml
---
screen_id: today
screen_name: Today
platform: iOS
framework: SwiftUI
target_os: iOS 26
device_frame: iPhone portrait, 402 x 874 pt
appearance: Light Mode
content_state: populated
status: approved-for-visual-generation
---
```

`target_os` menjelaskan keluarga desain yang harus diikuti oleh image-generation agent. Deployment target aktual tetap mengikuti Xcode project dan dicatat terpisah agar dokumen visual tidak mengarang API requirement.

### Visual direction

- 70% Organic Minimalism.
- 20% Clinical Clarity.
- 10% Playful Food Personality.
- Canvas off-white, surface putih, evergreen sebagai brand, amber/tomato sebagai aksen urgency.
- Foto atau ilustrasi makanan menjadi sumber warna utama.
- Native iOS, tenang, hangat, transparan, dan mudah dipindai.
- Status selalu memiliki teks atau ikon selain warna.

### Image-generation constraints

- Jangan menghasilkan Android, website, atau dashboard desktop.
- Jangan menambah fitur yang tidak tertulis.
- Jangan mengganti copy yang ditentukan.
- Jangan memenuhi seluruh background dengan hijau.
- Jangan memakai neon, gradient berat, glass berlebihan, atau kartu bertumpuk.
- Jangan menampilkan recipe, shopping list, nutrition score, atau statistik pada halaman yang tidak memintanya.
- Jangan menggunakan label `safe to eat`, `100% safe`, atau klaim keamanan absolut.

### External visual proposal workflow

1. Image-generation agent membaca `DESIGN_SYSTEM.md`, `VISUAL_GENERATION_GUIDE.md`, dan screen spec target.
2. Agent membuat gambar di luar percakapan ini.
3. Agent menghasilkan Markdown yang menjelaskan keputusan visual, asumsi, dan perbedaan dari spec.
4. Pengguna mengirim Markdown tersebut kembali ke Codex.
5. Codex membandingkan proposal dengan spec dan meminta keputusan untuk perubahan material.
6. Proposal disimpan di `VisualReferences/`; ia tidak menggantikan screen spec secara otomatis.
7. Setelah disetujui, keputusan dipindahkan ke design system atau screen spec sebelum coding UI.

## 12. Research Findings Applied

Desain agentic ini menerapkan hasil riset berikut:

- OpenAI menyarankan mulai dengan konteks, `AGENTS.md`, testing/review, lalu skill dan integrasi hanya setelah workflow berulang terbukti berguna.
- `AGENTS.md` paling efektif ketika singkat, praktis, dan memuat layout, build/test commands, constraints, serta definition of done.
- Skill adalah format authoring workflow reusable; plugin adalah unit distribusi bila workflow perlu dibagikan atau dibundel dengan connector.
- Subagent efektif untuk kerja independen atau noisy, tetapi menggunakan lebih banyak token. Review read-only adalah penggunaan yang jelas dan terbatasi.
- Execution plan berguna untuk pekerjaan panjang dan harus tetap menjadi living document.
- GitHub Spec Kit menguatkan urutan sederhana `Spec → Plan → Tasks → Implement`, tetapi paket lengkapnya tidak diperlukan untuk proyek ini.
- Pola agent yang andal menggunakan feedback environment seperti build dan tests, memiliki stopping condition, serta meningkatkan kompleksitas hanya bila hasil membaik secara nyata.

## 13. Deferred Capabilities

Capability berikut sengaja ditunda:

- custom plugin Fresh;
- MCP server;
- hooks dan scheduled automation;
- lebih dari satu custom reviewer role;
- proactive parallel implementation agents;
- Spec Kit installation;
- GitHub, Figma, atau cloud connector;
- release automation.

Capability dapat ditambahkan setelah workflow manual stabil atau kebutuhan berulang terbukti.

## 14. Git and GitHub Workflow

### Fondasi saat ini

- G00 boleh di-commit langsung ke `main` karena membentuk baseline pertama repo.
- Pesan commit yang direncanakan: `chore: establish Fresh agentic project foundation`.
- Sebelum commit, periksa `git status`, diff, file rahasia, validasi dokumentasi, dan verdict reviewer fresh terakhir.
- Push hanya dilakukan ke remote milik repo `/Users/ibnutaufickahraza/Swift/Fresh`. Jangan pernah menjalankan operasi Git dari repo lain.
- Local `origin` saat ini menunjuk ke `https://github.com/Ibnuck/Fresh.git`. Keberadaan, ownership, visibility, dan keadaan remote harus diverifikasi lagi sebelum push karena agent utama belum dapat mengakses GitHub dan `gh` belum tersedia.

### Goal berikutnya

```text
main
  └── dev
       ├── feature/g01-app-shell
       ├── feature/g02-freshness-domain
       └── feature/gxx-nama-singkat
```

- `main`: baseline stabil yang sudah disetujui.
- `dev`: integrasi goal yang sudah lulus quality gate tetapi belum menjadi milestone main.
- `feature/gXX-nama-singkat`: satu branch per goal pada tabel roadmap.
- Branch feature dibuat dari `dev` terbaru dan hanya memuat scope goal tersebut.
- Sesuai kebijakan proyek Fresh yang diperbarui pada DEC-010, agent tidak menjalankan operasi Git/GitHub yang mengubah state, baik sebelum maupun setelah quality gate. Agent hanya melakukan pemeriksaan read-only dan menyiapkan manual handoff setelah gate bersih.
- Quality gate wajib: scope/diff benar, tidak ada secret, acceptance criteria terpenuhi, build/test relevan lulus, hasil verifikasi tercatat, dan reviewer sub-agent fresh terakhir memberi `Verdict: No material findings`.
- Jika reviewer menemukan masalah, perbaiki temuan valid, jalankan ulang verifikasi, lalu gunakan reviewer fresh baru. Reviewer lama tidak boleh mengesahkan hasil perbaikannya sendiri.
- Setelah quality gate bersih, berikan kepada owner branch/base, exact staged paths, commit message, perintah pemeriksaan/staging/commit/push, serta draft PR title/body menuju `dev`. Owner menjalankan semuanya secara manual.
- Merge ke `dev` dilakukan hanya setelah PR checks/review yang berlaku juga bersih.
- Promotion `dev` ke `main` dilakukan pada milestone yang disetujui pengguna, bukan otomatis setiap commit.
- Agent boleh merencanakan branch, commit, push, dan PR hanya untuk repo Fresh ini, tetapi tidak mengeksekusinya. Operasi destructive, perubahan remote, dan autentikasi tidak disarankan atau dijalankan oleh agent.

## 15. Success Criteria Setup

Setup agentic dianggap berhasil ketika:

- Codex otomatis memahami struktur dan batas proyek dari `AGENTS.md`;
- mini-feature baru menghasilkan spec dan plan sebelum implementation;
- build/test commands dapat dijalankan secara reproducible;
- `AGENTS.md`, roadmap, dan workflow dapat memicu feature loop yang sama di percakapan baru tanpa skill duplikat;
- reviewer agent baru dapat mengaudit perubahan tanpa write access;
- review loop berhenti dengan alasan yang jelas, bukan tanpa batas;
- screen specs cukup eksplisit untuk menghasilkan proposal visual yang konsisten;
- struktur tetap mudah dipahami dan dirawat oleh satu developer.

## 16. Sources

### OpenAI and Codex

- [OpenAI Codex best practices](https://learn.chatgpt.com/guides/best-practices)
- [Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)
- [Build skills](https://learn.chatgpt.com/docs/build-skills)
- [Plugins](https://learn.chatgpt.com/docs/plugins)
- [Subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents)
- [Using PLANS.md for multi-hour problem solving](https://developers.openai.com/cookbook/articles/codex_exec_plans)

### Related agentic practices

- [AGENTS.md open format](https://agents.md/)
- [GitHub Spec Kit](https://github.com/github/spec-kit)
- [Anthropic: Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)
- [Swift Agent Skills catalog](https://github.com/twostraws/swift-agent-skills)
- [SwiftUI Agent Skill](https://github.com/twostraws/SwiftUI-Agent-Skill)
- [SwiftData Agent Skill](https://github.com/twostraws/SwiftData-Agent-Skill)
- [Swift Concurrency Agent Skill](https://github.com/twostraws/Swift-Concurrency-Agent-Skill)
- [Swift Testing Agent Skill](https://github.com/twostraws/Swift-Testing-Agent-Skill)

### Existing Fresh research

- `Fresh/Docs/APP_CONCEPT_RESEARCH.md`
- `Fresh/Docs/UI_UX_DESIGN_RESEARCH.md`
