---
screen_id: settings
screen_name: Settings
platform: iOS
framework: SwiftUI
target_os_design_language: iOS 26
reference_device: iPhone portrait 402x874pt
appearance: Light Mode
content_state: default
status: approved-for-visual-generation
version: 1
---

# Settings

## 1. Outcome

Pengguna dapat mengendalikan pengingat, format tanggal, privacy, sumber aturan, onboarding, dan status intelligence tanpa halaman pengaturan yang berlebihan.

## 2. Entry, exit, and primary action

- Entry: gear toolbar from Today/My Food.
- Presentation: NavigationStack pushed page or sheet; use pushed page with back in visual proposal.
- Settings save immediately only when system operation succeeds; errors are visible.
- Destinations: notification detail/system settings, privacy explanation, freshness sources, onboarding.

## 3. Three-second hierarchy

1. Title `Pengaturan`.
2. Pengingat.
3. Preferensi tanggal.
4. Privacy/intelligence transparency.
5. About/reset controls.

## 4. Top-to-bottom grouped form

### Section A — Pengingat

- Header `Pengingat`.
- Toggle row `Ingatkan bahan yang perlu digunakan` → on in default mockup.
- Scheduling row `Waktu pengingat` → `09.00` with disclosure/time picker.
- If permission denied, do not show enabled toggle as success. Show amber/slate inline message:
  `Notifikasi dimatikan untuk Fresh.` and button `Buka Pengaturan iPhone`.
- Footer `Pengingat mengikuti estimasi yang dapat berubah saat data bahan diperbarui.`

### Section B — Tampilan tanggal

- Row `Format tanggal` → `12 Agu 2026`.
- Options later: system default, day-month-year; no need to show picker in primary screenshot.

### Section C — Privacy dan intelligence

- Navigation row `Privacy` with shield icon.
- Row `Interpretasi pintar di perangkat` with status value `Tersedia` or `Tidak tersedia` rather than toggle if availability is system-defined.
- Footer `Jika digunakan, interpretasi berjalan di perangkat. Fresh tetap berfungsi tanpa fitur ini.`
- Do not use Apple Intelligence logo unless permitted by actual product guidelines; SF Symbol is safer.

### Section D — Tentang estimasi

- Navigation row `Sumber panduan kesegaran`.
- Supporting footer `Estimasi membantu menentukan prioritas penggunaan dan bukan jaminan keamanan pangan.`

### Section E — Onboarding and reset

- Button row `Ulangi onboarding`.
- Destructive button `Hapus semua data Fresh…` separated with confirmation. This action is optional/deferred for MVP implementation but may be listed only if roadmap accepts it; primary visual should omit it to keep current MVP scope safe.
- Version row `Fresh` → `Versi 1.0` at bottom.

## 5. Component inventory

| Component | SwiftUI mapping | Behavior |
|---|---|---|
| Page | `Form` with sections | Native grouped appearance. |
| Reminder | `Toggle`, `DatePicker` | Permission-aware; failures visible. |
| Navigation rows | `NavigationLink` | Privacy/source detail. |
| Status value | `LabeledContent` | Availability text, not color only. |
| Reset onboarding | `Button` | Presents onboarding without deleting food. |

## 6. States

- Notification permission not determined: toggle attempt triggers system prompt at appropriate moment, not on onboarding launch.
- Denied: inline message and system-settings link.
- Scheduling failure: keep selected preference but show `Pengingat belum dapat dijadwalkan. Coba lagi.`
- Intelligence unavailable: value `Tidak tersedia di perangkat ini`; no blocking alert.
- Large Dynamic Type: labels wrap and values move below; form remains native.
- Dark Mode: use system grouped surfaces and semantic colors.

## 7. Accessibility

- Toggle announces current on/off and full label.
- Status `Tidak tersedia` is text, not disabled opacity alone.
- Footers remain readable and are not tiny low-contrast legal copy.
- System settings button describes destination.

## 8. Do not include

- Account, subscription, cloud sync, household sharing, developer/debug menus, theme picker, recipe preferences, nutrition goals, or analytics dashboard.

## 9. Requested outputs

- Canonical: `settings_default_light_v01.png`.
- Notification denied, Dark Mode, permission feedback, and unavailable-intelligence states are specified in Markdown and verified during SwiftUI implementation.
