# Fresh Product Roadmap

Roadmap ini menjelaskan outcome, bukan deadline. Satu goal = satu feature branch setelah G00.

| Goal | Branch | Ringkasan hasil | Quality gate utama |
|---|---|---|---|
| G00 Agentic Foundation | `main` baseline | Chat coding baru memahami proyek, keputusan, visual spec, workflow, skills, review, dan Git policy; prosesnya dapat dipakai ulang untuk proyek baru. | Dokumen/skills valid dan reviewer fresh final bersih. |
| G01 App Shell | `feature/g01-app-shell` | Aplikasi launch dengan root navigation dan dependencies stabil. | Build + launch smoke + navigation check. |
| G02 Freshness Domain | `feature/g02-freshness-domain` | Status freshness deterministik dan dapat dijelaskan. | Boundary/timezone/missing-data unit tests. |
| G03 Onboarding | `feature/g03-onboarding` | Pengguna memahami manfaat, bisa skip, dan menuju item pertama. | State persistence + accessibility + UI flow. |
| G04 Core Empty States | `feature/g04-core-empty-states` | Today/My Food dapat dinavigasi dan empty state memandu tindakan. | UI states + VoiceOver + Dynamic Type. |
| G05 Add and Estimate | `feature/g05-add-and-estimate` | Bahan minimal dapat ditambah, asumsi ditinjau, unknown tetap unknown. | Draft/error persistence + form/flow tests. |
| G06 Live Inventory | `feature/g06-live-inventory` | Data nyata muncul dan dikelompokkan menurut urgensi. | SwiftData integration + search/filter/regroup. |
| G07 Food Lifecycle | `feature/g07-food-lifecycle` | Detail, alasan estimasi, edit/use/freeze/move/discard bekerja. | State transitions + regression + failure recovery. |
| G08 Reminders and Settings | `feature/g08-reminders-settings` | Pengguna mengendalikan reminder, format, privacy, dan settings. | Permission/error boundaries + persistence. |
| G09 Optional Intelligence | `feature/g09-optional-intelligence` | AI on-device membantu input tetapi tidak menjadi ketergantungan. | Unavailable/invalid/fallback coverage. |
| G10 Release Quality | `feature/g10-release-quality` | MVP lolos regression, accessibility, visual, dan dokumentasi final. | Full suite + simulator/visual matrix + final fresh review. |

Detail acceptance criteria dibuat dalam spec/plan goal saat goal dimulai. Perubahan roadmap material membutuhkan persetujuan pengguna.
