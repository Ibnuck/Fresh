---
proposal_for_screen: today
proposal_version: 2
generator: Codex image generation
generated_at: 2026-08-13
source_spec_version: 1
approval_status: approved
---

# Generated UI Proposal — Today

## Assets

| State | Appearance | Image file/path | Status |
|---|---|---|---|
| Populated | Light | `../Screens/today_populated_light_v02.png` | **Canonical** visual anchor; fresh reviewer returned no material findings. |
| Populated, superseded | Light | `../Screens/today_populated_light_v01.png` | Preserved review history; do not implement. |
| Empty | Light | `../Screens/today_empty_light_v01.png` | Supplementary state reference; not a competing canonical design. |
| Populated | Dark | `../Screens/today_populated_dark_v01.png` | Supplementary appearance reference; not a competing canonical design. |

Reusable illustration assets are tracked separately under `../Illustrations/`. Mockups define composition; runtime implementation should use reviewed transparent assets rather than crop food images from a screen bitmap. `food_thumbnail_bayam_transparent.png` and `food_thumbnail_susu_transparent.png` are approved only for thumbnail/row use at approximately `56–64 pt`; Food Detail will receive its own hero asset rather than upscaling either thumbnail.

## Visual summary

The populated Light screen establishes Fresh's UI anchor: a warm off-white native iOS canvas, dark evergreen typography, restrained tomato and amber urgency, soft sage guidance, and a limited vivid orange Add accent inherited from the final app icon. The three-second hierarchy is title → Bayam priority → Susu segar → small actionable suggestion → bottom navigation. Food imagery supplies organic personality without turning the page into a commercial food catalogue.

## SwiftUI hierarchy

```text
NavigationStack
├── ScrollView
│   └── LazyVStack(alignment: .leading, spacing: 24)
│       ├── contextText
│       ├── prioritySection
│       │   ├── sectionHeader("Gunakan hari ini", "Lihat semua")
│       │   └── PriorityFoodCard(Bayam)
│       ├── soonSection
│       │   ├── sectionHeader("Segera gunakan")
│       │   └── FoodRow(Susu segar)
│       └── SuggestionStrip
├── toolbar
│   └── settingsButton
└── TabView / app-level bottom navigation
    ├── Hari ini (selected)
    ├── Tambah (global sheet action)
    └── Makananku
```

Use native large-title navigation behavior rather than manually fixing the title inside the scroll content. The generated bitmap captures the expanded state.

## Layout decisions

| Region | Position/size intent | Spacing/alignment | SwiftUI mapping | Behavior |
|---|---|---|---|---|
| Status/navigation | Top safe area; expanded large title; toolbar control minimum `44 × 44 pt` | Leading title; trailing gear | `.navigationTitle("Hari ini")`, `.navigationBarTitleDisplayMode(.large)`, `ToolbarItem` | Large title collapses natively on scroll. Gear accessibility label: `Buka pengaturan`. |
| Context line | Full content width below title; content-driven height | Main horizontal inset `20 pt`; approx. `8–12 pt` below title | `Text` `.subheadline` | May wrap at large text sizes; never truncate. |
| Use Today header | Full content width | Leading/trailing alignment; approx. `24–32 pt` above card | `HStack`, `Spacer`, text button | `Lihat semua` opens My Food and announces destination. |
| Bayam priority card | Full content width; approx. `112 pt` in the approved bitmap; minimum `104 pt` | Internal padding approx. `16 pt`; radius `16 pt` | One `Button`/`NavigationLink` containing adaptive stack | At larger text sizes, center/trailing areas become vertical and card height grows. Whole surface is tappable. |
| Bayam thumbnail | Approx. `64 × 64 pt`; aspect fit | Leading, vertically centered | Decorative `Image` with `.scaledToFit()` | Hide image from VoiceOver because the combined row identifies Bayam. |
| Bayam content | Content-driven | Name → metadata `4–6 pt`; badge below approx. `8 pt` | `VStack(alignment: .leading)` | Exact raw metadata remains legible; no clipping. |
| Bayam countdown | Intrinsic width | Trailing with chevron; moves below center content when needed | Adaptive `ViewThatFits`/layout | Combined accessible value includes estimate context. |
| Use Soon | Approx. `24 pt` after priority card | Leading section title | `VStack` | Remains visually subordinate to Bayam. |
| Susu row | Full content width; content-driven, minimum approx. `112 pt` in anchor | Padding approx. `16 pt`; thin neutral border/radius `16 pt` | Reusable `FoodRow` | Can collapse toward the Design System's `72 pt` minimum if the badge is placed efficiently; grows for Dynamic Type. |
| Suggestion | Full content width; content-driven | Sage surface; padding `16 pt`; icon leading; text gap `12–16 pt` | Semantic `HStack`/adaptive `VStack` | Static guidance; no recipe link. Body may wrap. |
| Bottom navigation | Anchored to bottom safe area; native-height intent; each target ≥ `44 pt` | Three equal destinations; central action emphasized | App-level `TabView` plus central sheet action | Selection persists. Add presents Quick Add without becoming a fourth content destination. |

## Typography

| Element | SwiftUI role | Visual intent |
|---|---|---|
| `Hari ini` | `.largeTitle.bold()` | Primary screen orientation. |
| Section headers | `.title3.weight(.semibold)` | Clear grouping without dashboard density. |
| Food names | `.headline` or `.title3.weight(.semibold)` where space permits | Highest row identity. |
| Metadata | `.subheadline` | Essential secondary context. |
| Status badges | `.subheadline.weight(.medium)` | Readable urgency label, not caption-sized. |
| Countdown | `.headline` | Important value with status context. |
| Suggestion body | `.body` or `.subheadline` | Actionable and comfortably readable. |
| Tab labels | Native tab label style | Never use orange below contrast threshold. |

## Tokens and contrast

| Pairing | Foreground | Background | Use |
|---|---|---|---|
| Primary | `#18201B` | `#F7F5EF` / `#FFFFFF` | Title, food names. |
| Secondary | `#667068` | `#F7F5EF` / `#FFFFFF` | Context and metadata. |
| Brand | `#1F6B4F` | `#F7F5EF` / `#FFFFFF` / `#DDEADF` | Selected Today, settings, links. |
| Use Today | `#C94B3B` | very pale tomato tint / white | Badge and `Hari ini`; always paired with words/icon. |
| Use Soon text | dark amber approx. `#8A4600`–`#944A00` | white / pale amber | Badge and `2 hari`; v02 bitmap sampling measured approx. `4.8:1` for countdown. |
| Add label | dark burnt orange approx. `#8A3D00` | white | v02 bitmap sampling measured approx. `6.7:1`; the circular plus may remain vivid `#FF8D28`. |
| Suggestion | `#1F6B4F` and `#18201B` | `#DDEADF`-direction surface | Leaf/lightbulb and text. |

Target normal-text contrast is at least `4.5:1`. The bitmap is a visual proposal; implementation must use semantic/adaptive tokens and recheck actual rendered contrast in Light, Dark, and Increase Contrast.

## Interaction model

- Tapping the full Bayam card opens Food Detail for Bayam.
- Tapping the full Susu row opens Food Detail for Susu segar.
- `Lihat semua` switches/navigates to My Food.
- Gear opens Settings.
- `Tambah` presents Quick Add.
- Suggestion is informational and has no tap action in MVP.
- Local content should appear immediately; do not show a spinner by default.

## State adaptations

- Empty Light uses the same navigation shell, places the reviewed transparent basket illustration slightly above optical center, and presents the exact empty title, explanatory body, primary `Tambahkan bahan` action, and concise minimum-input note. A context-clean reviewer found no material issue at normal iPhone viewing size.
- Populated Dark preserves the Light anchor's content, order, hierarchy, and proportions while adapting the canvas to warm evergreen-charcoal, using restrained elevated surfaces and accessible adaptive urgency colors. Representative ordinary-text samples measured approximately `5.26:1` to `10.93:1` in its context-clean review.
- Read failure replaces food sections with `Makananmu belum dapat dimuat` and `Coba lagi`, while navigation remains available.
- All-caught-up uses `Tidak ada yang mendesak hari ini`; it does not fabricate urgent items.
- Large Dynamic Type: cards/rows become vertical, metadata wraps, countdown stays adjacent to its item, suggestion icon may align top, and tab labels follow native behavior.
- Reduce Motion: insert/regroup changes use a short fade rather than large movement; countdown never pulses.

## Accessibility annotations

VoiceOver order: title/context → settings only when reached through toolbar order → Use Today header/action → Bayam row → Use Soon → Susu row → suggestion → app-level tabs.

- Bayam combined label/value: `Bayam, gunakan hari ini, hari ini, disimpan di kulkas, dicuci dan dibuka.`
- Susu combined label/value: `Susu segar, segera gunakan, perkiraan dua hari, disimpan di kulkas, dibuka kemarin.`
- `Lihat semua` hint: `Membuka semua bahan di Makananku`.
- Settings: `Buka pengaturan`.
- Food images are hidden as separate VoiceOver elements when the row already names the item.
- Status includes words and a clock/semantic cue rather than color alone.

## Compliance matrix

| Requirement | Met in v02? | Evidence |
|---|---|---|
| Correct title/context | Yes | Top hierarchy uses exact copy. |
| Bayam is the prominent Use Today item | Yes | First full-width priority card. |
| Bayam thumbnail approx. `64 pt` | Yes | Reviewer found a plausible 64 pt thumbnail frame after v02 repair. |
| Susu is the only Use Soon item | Yes | One lower-emphasis row with exact data. |
| Exact suggestion | Yes | Sage strip contains exact title/body. |
| Exactly three bottom destinations | Yes | `Hari ini`, `Tambah`, `Makananku`; Settings remains toolbar-only. |
| Search absent | Yes | No search control appears. |
| Status not color-only | Yes | Text and clock cues accompany colors. |
| Normal orange text contrast | Yes | Reviewer sampled approx. `4.8:1` (`2 hari`) and `6.7:1` (`Tambah`). |
| No out-of-scope feature | Yes | No recipe, analytics, shopping, nutrition, chat, category, or extra item. |

## Review history

1. v01 reviewer found two P2 issues: low-contrast orange ordinary text and an oversized ~100 pt Bayam visual.
2. v02 reduced the Bayam image toward 64 pt, tightened the card, and darkened ordinary orange text.
3. A different context-clean reviewer returned `Verdict: No material findings.`
4. Empty Light v01 was compared with the Today spec, approved populated shell, transparent illustration, visual style lock, UI mood reference, and app-icon palette; its context-clean reviewer returned `Verdict: No material findings.`
5. Populated Dark v01 was checked against the same contracts and the approved Light anchor, including representative contrast samples; its context-clean reviewer returned `Verdict: No material findings.`

## Assumptions

- The screen bitmap is treated as the expanded large-title state.
- Card heights remain content-driven in SwiftUI even though approximate visual dimensions are documented.
- The generated food assets are illustration references; actual photos remain decorative and optional.

## Deviations from source spec

None material in the approved populated Light proposal. The Susu row is visually more card-like and taller than the system's minimum FoodRow, but it remains functionally one non-nested row and must be allowed to compact/adapt during implementation.

## Decisions needed

None for populated Light.

## Suggested spec updates

None. This proposal implements the current source spec; it does not replace it.
