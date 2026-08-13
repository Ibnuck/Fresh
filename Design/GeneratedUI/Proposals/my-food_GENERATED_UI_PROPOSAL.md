---
proposal_for_screen: my-food
proposal_version: 3
generator: Codex image generation
generated_at: 2026-08-13
source_spec_version: 2
approval_status: canonical-approved
---

# Generated UI Proposal — My Food

## Canonical assets and authority

| State | Appearance | Image file/path | Status |
|---|---|---|---|
| Populated | Light | `../Screens/my-food_populated_light_v04.png` | **Canonical** composition; fresh reviewer returned no material findings. |
| Populated, superseded | Light | `../Screens/my-food_populated_light_v01.png`–`v03.png` | Review history; do not implement geometry from these files. |
| Search empty | Light | `../Screens/my-food_search-empty_light_v01.png` | Supplementary state reference; fresh reviewer returned no material findings. |
| Dynamic Type | Light | Not generated | Defined here and in the screen spec; verify in native SwiftUI. |

Implementation priority is: `Fresh/Docs/ScreenSpecs/03_MY_FOOD.md` → `Fresh/Docs/DESIGN_SYSTEM.md` → this proposal → canonical bitmap. The bitmap establishes hierarchy and visual rhythm; it does not override exact copy, native safe areas, or adaptive behavior.

## Measurement conventions

- Reference viewport: `402 × 874 pt` iPhone portrait. The `851 × 1848 px` bitmap is approximately a `2×` visual reference, not an absolute-coordinate specification.
- Values labeled `approx.` may move by one spacing-grid step during native implementation.
- Values labeled `minimum` are accessibility/interaction constraints and must not shrink.
- Heights are `content-driven` unless explicitly stated; Dynamic Type may increase them.
- Main horizontal content inset: `20 pt`; common vertical spacing: `8, 12, 16, 20, 24 pt`.
- Respect the system status/navigation safe area and bottom home-indicator safe area. Do not reproduce status-bar pixels manually.

## Visual summary

My Food is a calm, searchable inventory rather than a dashboard. The three-second hierarchy is `Makananku` → search → storage filters → urgency groups. The canonical frame uses four compact urgency sections so Bayam, Susu, Tempe, and Alpukat remain scannable, while the bottom app navigation stays visually separate from scroll content. Search exists only on this screen.

## SwiftUI view tree

```text
NavigationStack
├── inventoryContent
│   └── ScrollView / List
│       ├── SearchField("Cari bahan")
│       ├── ScrollView(.horizontal, showsIndicators: false)
│       │   └── HStack(spacing: 8–12)
│       │       ├── StorageChip("Semua", selected: true)
│       │       ├── StorageChip("Kulkas")
│       │       ├── StorageChip("Freezer")
│       │       └── StorageChip("Dapur")
│       └── LazyVStack(alignment: .leading, spacing: 16–20)
│           ├── UrgencySection(useToday, Bayam)
│           ├── UrgencySection(useSoon, Susu segar)
│           ├── UrgencySection(fresh, Tempe)
│           └── UrgencySection(needsReview, Alpukat)
├── toolbar
│   └── SettingsButton
└── AppTabBar
    ├── Hari ini (unselected)
    ├── Tambah (global sheet action)
    └── Makananku (selected)
```

Use one native scrolling owner for search, filters, and inventory. Do not nest a vertically scrolling `List` inside another vertical `ScrollView`. A styled `List` with custom section headers is preferred when it preserves native accessibility and row behavior; otherwise use one `ScrollView` + `LazyVStack`.

## Region-by-region layout

| Region | Position and frame intent | Padding, spacing, alignment | Distribution | SwiftUI mapping and behavior |
|---|---|---|---|---|
| Status/navigation | Native top safe area; expanded large title; Settings target minimum `44 × 44 pt` | Title leading; gear trailing; main content begins approx. `12–16 pt` after large-title region | Title consumes flexible width; gear intrinsic | `.navigationTitle("Makananku")`, large display mode, trailing `ToolbarItem`; title collapses natively while scrolling. |
| Search | Full content width inside `20 pt` inset; approx. `50–54 pt` default height; radius approx. `12 pt` | Magnifier leading `12–16 pt`; text gap `8–10 pt`; optional clear button trailing | Text field expands; icons remain intrinsic | Native `.searchable` when its placement matches the canonical frame, or a labeled `TextField`; placeholder exact `Cari bahan`. |
| Filter scroller | Directly below search, approx. `16–20 pt` vertical gap; one horizontal line | Outer horizontal inset `20 pt`; chip gap `8–12 pt`; preserve trailing scroll breathing room `20 pt` | Chips intrinsic width, never equal-width stretched | Horizontal `ScrollView`; each chip minimum height `44 pt`, horizontal padding approx. `16–18 pt`, capsule shape. |
| Selected chip | `Semua`, approx. `44–48 pt` high | Text and optional checkmark centered; internal gap `6–8 pt` | Content centered | Brand-soft fill, evergreen text/checkmark; announce selected state. |
| Inventory stack | Below chips with approx. `24–28 pt` first gap; full content width | Main inset `20 pt`; section-to-section gap approx. `16–20 pt` in canonical default | Vertical, stable urgency order | Sections with zero visible rows are hidden; searching/filtering preserves order. |
| Section header | Full width; content-driven, minimum target-height intent `32–44 pt` | Header-to-row gap approx. `6–8 pt`; baseline/first-text alignment | Urgency label leading; count `1` trailing, intrinsic | `HStack { Label/Text; Spacer(); count }`; mark as accessibility heading. |
| Food row surface | Full width; canonical approx. `92–96 pt`, implementation minimum `72 pt`; radius approx. `16 pt` | Internal horizontal padding approx. `12–16 pt`; vertical padding approx. `10–12 pt` | Leading thumbnail; flexible center; intrinsic trailing status/chevron | One `NavigationLink`/`Button`; use subtle surface/border, not nested cards. Entire row is one target. |
| Thumbnail | Approx. `48–56 pt` square, aspect fit | Leading, vertically centered; gap to text approx. `12–16 pt` | Fixed proposal width; never stretches | Decorative `Image`, `.scaledToFit()`, hidden from VoiceOver because row label names the food. |
| Text column | Flexible width; content-driven | `VStack(alignment: .leading, spacing: 4–6)` | Highest layout priority; metadata wraps before truncating | Name → metadata → status line. At accessibility sizes it may occupy a new vertical row. |
| Trailing value | Intrinsic width, proposal max around `72–88 pt` before reflow | Gap from text approx. `8–12 pt`; chevron gap `6–8 pt` | Countdown/status trailing, vertically centered | `ViewThatFits` or custom adaptive layout; move below content when horizontal fit fails. |
| Bottom navigation | Anchored outside inventory scroll at bottom safe area; native-height intent; rounded system material in visual proposal | Three destinations each minimum `44 pt`; home-indicator inset handled by system | Three equal logical slots; center Add emphasized; My Food selected | App-level tab/navigation container. Add presents Quick Add and is not a fourth destination. Scroll content receives bottom inset so Alpukat never sits beneath the bar. |

## Food-row content contracts

| Group | Name | Metadata | Status/value | Visual cue |
|---|---|---|---|---|
| `Gunakan hari ini  1` | `Bayam` | `Kulkas • Dicuci, dibuka` | `Gunakan hari ini` / `Hari ini` | Tomato text + clock; never color alone. |
| `Segera gunakan  1` | `Susu segar` | `Kulkas • Dibuka kemarin` | `Segera gunakan` / `2 hari` | Dark amber text + clock. |
| `Masih fresh  1` | `Tempe` | `Kulkas • Kemasan tertutup` | `Masih fresh` / `4 hari` | Leaf green text + checkmark. |
| `Perlu ditinjau  1` | `Alpukat` | `Dekat jendela • Lokasi belum dipahami` | `Tinjau` | Slate text + question/check cue; no warning triangle. |

## Typography

| Element | SwiftUI style | Weight/alignment | Adaptation |
|---|---|---|---|
| Navigation title | `.largeTitle` | `.bold`, leading | Native large-title collapse; maximum two lines only if localization requires it. |
| Search text | `.body` | regular, leading | Never scale below body; clear button remains reachable. |
| Filter chip | `.subheadline` | `.medium`, centered | Intrinsic width grows with text; no truncation. |
| Section heading | `.title3` | `.semibold`, leading | Count uses `.subheadline`/`.body`, trailing. |
| Food name | `.headline` | `.semibold`, leading | Highest text priority inside row. |
| Metadata | `.subheadline` | regular, leading | Wrap to two lines before truncation. |
| Status label | `.subheadline` | `.medium`, leading | Icon and words remain together where possible. |
| Countdown/`Tinjau` | `.headline` | `.medium` or `.semibold`, trailing | Moves below center content at large sizes. |
| Tab labels | native tab label style | system selection treatment | Do not manually shrink; respect Bold Text. |

## Color and material tokens

| Role | Light | Dark | Pairing/use |
|---|---|---|---|
| Canvas | `#F7F5EF` | `#111612` | Screen background. |
| Surface | `#FFFFFF` | `#1B211D` | Search, row, tab/material direction. |
| Primary text | `#18201B` | `#F3F5F1` | Title, names, headings. |
| Secondary text | `#667068` | `#AAB3AC` | Search placeholder, metadata, counts. |
| Brand | `#1F6B4F` | `#5DBB8E` | Settings, selected chip/tab, links. |
| Brand soft | `#DDEADF` | `#244232` | Selected chip and selection surface. |
| Use Today | `#C94B3B` | `#F27868` | Text/icon with a very light corresponding tint. |
| Use Soon | darkened amber approx. `#8A4600`–`#944A00` | `#E7A542` | Ordinary text must meet `4.5:1`; do not use the brighter raw icon orange for small text. |
| Fresh | `#4B7D45` | `#81BE78` | Tempe status/check. |
| Needs Review | `#58708A` | `#91A9C1` | Alpukat status/question. |
| Divider/border | `#E4E5DF` | `#343B36` | Subtle `1 px`/hairline native separator direction. |
| Global Add | vivid `#FF8D28` circle; darker accessible label | adaptive warm orange | Limited icon-derived accent only. |

Use semantic/adaptive `Color` definitions rather than hard-coded appearance checks in views. Target normal-text contrast `≥ 4.5:1`; Increase Contrast strengthens borders and foregrounds without adding saturated card fills. Shadows remain extremely subtle or absent.

## Reusable assets and image rules

- `food_thumbnail_bayam_transparent.png`
- `food_thumbnail_susu_transparent.png`
- `food_thumbnail_tempe_transparent.png`
- `food_thumbnail_alpukat_transparent.png`

These are row thumbnails scoped to approximately `48–64 pt`, not detail heroes. Use aspect fit and preserve transparent padding. Do not crop a food image from the canonical bitmap.

The Tempe asset was repaired after the original chroma removal created holes in its cream texture. The standalone runtime PNG now uses a conservative border-connected matte and passed Light/Dark review at `64 pt`. The canonical layout bitmap predates that repair; use its layout but inject the repaired asset.

## Interaction model

- Entry is the `Makananku` bottom destination or `Lihat semua` from Today; both land on the same inventory state unless an existing search/filter state is intentionally preserved by app navigation.
- Typing in search filters names locally and preserves urgency sections while hiding empty groups.
- Selecting one storage chip changes the single active filter; `Semua` clears the storage filter.
- Tapping any full row opens Food Detail for that item.
- Tapping Settings opens Settings; `Tambah` presents Quick Add; `Hari ini` switches tabs.
- No pull-to-refresh is shown for local-only data. No swipe action is required for a primary lifecycle action.
- Search result changes should use a short cross-fade/regroup animation `150–250 ms`; Reduce Motion uses fade/no large movement.

## State adaptations

| State | Required behavior and layout |
|---|---|
| Search empty | Keep title, active query, clear button, chips, and tabs. Source template is exactly `Tidak ada hasil untuk “…”`; at runtime replace the ellipsis with the preserved query, for example `Tidak ada hasil untuk “tahu”`. Action: `Hapus pencarian`. |
| Filter empty | Keep selected chip/search. Show `Tidak ada bahan di freezer` and `Hapus filter`; do not imply global inventory is empty. |
| Global empty | No search results are fabricated. Show `Makananku masih kosong` and `Tambahkan bahan pertama`. |
| Read error | Keep navigation available; show `Makananmu belum dapat dimuat` and `Coba lagi`. |
| Loading | Local SwiftData should normally render immediately; only use redacted row placeholders for real asynchronous work, not a default spinner. |
| Dynamic Type | Chips remain horizontally scrollable. Row changes from three-column horizontal distribution to thumbnail + vertical content; trailing value moves below/adjacent to status. |
| Dark Mode | Preserve separator visibility and restrained surfaces; use adaptive status colors above. |
| Reduce Motion | Search/filter regroup uses opacity instead of large position animation. |

## Accessibility annotations

VoiceOver order: navigation title → Settings → search → filter chips left-to-right → urgency heading/count → row, repeated by section → bottom destinations.

- Search label: `Cari bahan`; clear action uses native accessible clear semantics.
- Chip value includes selected state, for example `Semua, dipilih`.
- Section headers use `.isHeader` and include count without forcing it to be read twice.
- Combine each row into one element. Examples:
  - `Bayam, gunakan hari ini, perkiraan hari ini, disimpan di kulkas, dicuci dan dibuka.`
  - `Tempe, masih fresh, perkiraan empat hari, disimpan di kulkas, kemasan tertutup.`
  - `Alpukat, perlu ditinjau, lokasi dekat jendela belum dipahami.`
- Decorative food images and disclosure chevrons are hidden as separate elements.
- All controls meet minimum `44 × 44 pt`; status never relies on color alone.
- Avoid announcing every search keystroke. Announce a settled result-count change after a short debounce only when useful.

## Compliance matrix

| Requirement from source spec | Met? | Evidence/implementation contract |
|---|---|---|
| Title, Settings, no item count | Yes | Canonical top region and navigation contract. |
| Search exists only on My Food | Yes | Search region is local to this screen; Today remains search-free. |
| Exact storage filters | Yes | `Semua`, `Kulkas`, `Freezer`, `Dapur`; single selection. |
| Stable four-group urgency order | Yes | View tree and row-content table. |
| Exact example data | Yes | Four content contracts above. |
| Rows, not four unrelated nested cards | Yes, with implementation clarification | Canonical surfaces are visually card-like, but implementation uses one flat row component per section and no nested cards. |
| Needs Review is calm slate | Yes | Slate token + question cue, never red warning. |
| Correct tab selection | Yes | Today unselected, Add central, My Food selected. |
| Search/filter/global/error states | Yes | State table defines distinct copy and recovery. |
| Dynamic Type and VoiceOver | Yes | Adaptive distribution and combined labels specified. |
| No prohibited feature | Yes | No grid/sort/bulk edit/recipe/prices/nutrition/store grouping. |

## Review history

1. v01 reviewer found the Alpukat row hidden beneath an incomplete bottom shell.
2. v02–v03 iterated safe-area spacing; v04 established a complete Alpukat row, canvas separation, rounded tab surface, and home indicator.
3. A different context-clean reviewer returned `Verdict: No material findings.` for v04.
4. The standalone Tempe alpha asset was subsequently repaired and separately returned `Verdict: No material findings.` at its intended row scale.

## Assumptions

- The canonical bitmap represents an expanded large-title, top-of-list state.
- Section/row heights remain content-driven even where canonical approximate values are listed.
- Native tab/search material may differ slightly by OS point release; hierarchy and contrast take priority over pixel matching.

## Deviations from source spec

| Deviation | Reason | User decision required? |
|---|---|---|
| Canonical rows use rounded individual surfaces more visibly than a minimal separator-only list. | Improves scan separation in the accepted visual. Implementation must keep them flat, non-nested, and compact. | No; accepted canonical direction. |

## Decisions needed

None.

## Suggested spec updates

None. This proposal supplies implementation measurements without changing product behavior.
