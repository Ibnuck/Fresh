# Fresh Visual Style Lock

## Status

- Date: 2026-08-13
- State: approved direction; canonical-screen generation in progress
- Visual anchor: Today populated, Light Mode
- Source priority: target screen spec → Design System → Visual Generation Guide → reconciliation → visual references

## Character

Fresh uses calm native iOS clarity with warm organic food personality. Screens stay spacious and practical; illustration depth and rounded organic forms echo the Sprout & Slice icon without repeating the complete app-icon composition.

## Color lock

| Role | Light | Dark | Usage |
|---|---|---|---|
| Canvas | `#F7F5EF` | `#111612` | Main app background. |
| Surface | `#FFFFFF` | `#1B211D` | Functional cards, rows, and sheets. |
| Primary text | `#18201B` | `#F3F5F1` | Titles and essential values. |
| Secondary text | `#667068` | `#AAB3AC` | Metadata and explanations. |
| Brand evergreen | `#1F6B4F` | `#5DBB8E` | Primary CTA, selection, focus. |
| Brand soft | `#DDEADF` | `#244232` | Calm supporting surface. |
| Icon orange | `#FF8D28` | `#E88432` | Limited warm accent and global Add emphasis; never the entire UI canvas. |
| Use Today | `#C94B3B` | `#F27868` | Highest urgency with text/icon. |
| Use Soon | `#B66B13` | `#E7A542` | Near-term urgency with text/icon. |
| Fresh | `#4B7D45` | `#81BE78` | Fresh status with text/icon. |
| Needs Review | `#58708A` | `#91A9C1` | Unresolved information with text/icon. |
| Divider | `#E4E5DF` | `#343B36` | Subtle separators. |

Normal text targets at least 4.5:1 contrast. Orange is not used behind small white text unless the pairing is verified; evergreen remains the dependable primary-action color.

## Typography

Use San Francisco through Dynamic Type: `.largeTitle.bold()` for the screen title, `.title3.semibold()` for section titles, `.headline` for item names/buttons, `.body` for guidance, `.subheadline` for important metadata, and `.caption` only for noncritical supporting detail. Layout grows vertically at larger sizes; text is never reduced to force a fit.

## Geometry and material

- Reference canvas: iPhone portrait `402 × 874 pt`.
- Main horizontal inset: `20 pt`; spacing grid: `4 pt` with common values `8, 12, 16, 20, 24, 32`.
- Minimum hit target: `44 × 44 pt`.
- Field/small surface radius: `12 pt`; functional card radius: `16 pt`; status/chip: capsule.
- Borders and shadows are subtle. No nested floating cards or heavy glassmorphism.
- Liquid Glass appears only where iOS would naturally provide it, such as system bars/material transitions; content remains readable and mostly opaque.

## Image language

Food assets use the icon's soft organic rendering: clean silhouette, gentle tonal variation, warm highlights, restrained depth, and transparent surroundings. The full leaf–clock–tomato app icon is never reused as a generic hero. Food thumbnails are decorative within a combined accessible row and must be reused rather than regenerated per screen.

Visual QA is proportional to real use. Review thumbnails at `56–64 pt`, screen mockups at normal iPhone viewing size, and hero artwork at its own `180–220 pt` target. Microscopic source-pixel irregularities that are invisible at intended size are not blockers. A thumbnail must not be enlarged into a detail hero; create and review a dedicated higher-scale hero asset when the detail screen needs one.

## Canonical-screen rule

Generate one canonical default-content Light mockup for each screen. It is the only bitmap implementation anchor for that page. Alternate states—Dark Mode, empty/error/loading, search/filter results, keyboard, validation, Dynamic Type, and unavailable behavior—are defined in the screen specification and generated proposal, then completed and verified during SwiftUI implementation. Existing alternate-state images are supplementary references only.

Before a canonical screen is approved, verify not just its appearance but also the feature contract: how the user enters and leaves, which values the user types or selects, which values Fresh generates, what is saved, what the primary action does, and which claims/features are prohibited.

Small native UX improvements may be accepted from a generated proposal when they preserve that contract and are documented before implementation. Never let a visually attractive suggestion silently change core inputs, ownership of generated information, required/optional behavior, save timing, safety wording, or destination.

## Navigation and component lock

- Bottom navigation: `Hari ini`, central action `Tambah`, `Makananku`.
- Settings stays in the toolbar. Search exists only in My Food.
- `FoodRow` combines thumbnail, name, metadata, status text, countdown, and disclosure.
- Status never relies on color alone.
- One dominant CTA per viewport.
- Native SwiftUI navigation, sheets, keyboard, Form/List, and safe-area behavior.

## Continuity data

- Bayam — `Kulkas • Dicuci, dibuka` — `Gunakan hari ini` — `Hari ini`.
- Susu segar — `Kulkas • Dibuka kemarin` — `Segera gunakan` — `2 hari`.
- Tempe — `Kulkas • Kemasan tertutup` — `Masih fresh` — `4 hari`.
- Alpukat — `Dekat jendela • Lokasi belum dipahami` — `Perlu ditinjau` — `Tinjau`.

## Non-negotiable scope

No recipes, shopping list, nutrition, barcode/OCR, cloud sync, accounts, analytics, social features, safety verdicts, or unsupported statistics. Category is generated by Fresh; storage, condition, and package status are free text; ripeness is not a separate or inferred field; missing information remains unknown.
