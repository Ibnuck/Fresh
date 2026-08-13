---
proposal_for_screen: estimate-review
proposal_version: 2
generator: Codex image generation
generated_at: 2026-08-13
source_spec_version: 2
approval_status: canonical-approved
---

# Generated UI Proposal — Estimate Review

## Canonical assets and authority

| State | Image | Role |
|---|---|---|
| Estimate available — new Bayam draft | `../Screens/estimate-review_available_light_v01.png` | **Canonical** review-and-save hierarchy; context-clean reviewer returned no material findings. |

Needs Review, save error, disclosure expansion, Dark Mode, and Dynamic Type are implementation states defined here and in the source spec, not competing canonical screens. Small provenance/input icons in the bitmap are accepted semantic affordances; they improve scanning without changing information ownership.

Implementation priority is: `Fresh/Docs/ScreenSpecs/05_ESTIMATE_REVIEW.md` → `Fresh/Docs/DESIGN_SYSTEM.md` → this proposal → canonical bitmap. Exact copy, data provenance, safety wording, native safe areas, and adaptive layout override pixel matching.

## Measurement conventions

- Reference viewport: `402 × 874 pt` iPhone portrait. The raster is a visual anchor, not a fixed-coordinate layout.
- `Approx.` values may move by one `4 pt` spacing-grid step; `minimum` values must not shrink.
- Heights are content-driven. At large Dynamic Type, horizontal labeled content may become vertical.
- Main horizontal content inset: `20 pt`; common gaps: `8, 12, 16, 20, 24 pt`.
- The bottom save dock lives outside the scroll content and respects keyboard/home-indicator safe areas.

## Feature and information contract

Estimate Review is the boundary between the unsaved Quick Add draft and persisted food. It must let the user audit the estimate and its inputs before explicitly choosing `Simpan bahan`.

| Displayed information | Owner/source | Display rule |
|---|---|---|
| Name, raw storage, condition, package, reference type/date | User | Preserve exact entered wording and never relabel it as generated. |
| Category and normalized tags | `Interpretasi Fresh` | Derived through local matching and optional on-device interpretation; clearly identified and adjustable. |
| Urgency/countdown | Deterministic Fresh rule engine | Never derived from Foundation Model world knowledge. |
| Confidence/source | Fresh explanation | Human-readable word and rule source; no unexplained percentage. |
| Disclaimer | Fresh safety copy | Visible near the estimate; never hidden behind disclosure. |

Category appears here because the user did not enter it in Quick Add. Unstated ripeness, package status, condition, storage, or date remains unknown.

## Visual summary

The screen reads as a calm audit, not an AI verdict. The three-second hierarchy is `Bayam` → `Gunakan hari ini` / `Hari ini` → visible disclaimer → source and inputs → `Simpan bahan`. The hero stays compact and centered, while provenance and raw inputs use quiet white surfaces on the warm canvas. Evergreen owns actions and provenance; tomato indicates urgency only with words.

## SwiftUI view tree

```text
NavigationStack
├── ScrollView
│   └── LazyVStack(alignment: .leading, spacing: 20–24)
│       ├── EstimateHero
│       │   ├── FoodThumbnail(Bayam)
│       │   ├── Text("Bayam")
│       │   ├── UrgencyBadge("Gunakan hari ini")
│       │   ├── Text("Hari ini")
│       │   ├── Text("Perkiraan kualitas terbaik")
│       │   └── Disclaimer
│       ├── ProvenanceCard
│       │   ├── ConfidenceRow
│       │   ├── SourceRow
│       │   └── InterpretationLabel
│       ├── InputsSection("Berdasarkan")
│       │   └── LabeledInputRows
│       ├── DisclosureGroup("Mengapa estimasi ini?")
│       ├── SecondaryButton("Sesuaikan estimasi")
│       └── SupportingText
├── toolbar
│   ├── navigation: Back
│   ├── principal: Tinjau estimasi
│   └── cancellationAction: Batal (creation flow only)
└── safeAreaInset(edge: .bottom)
    ├── SaveError (conditional)
    └── PrimaryButton("Simpan bahan")
```

Use one vertical scrolling owner. The draft and derived review result live in feature state above the view hierarchy so Back/Adjust/save failure cannot discard them.

## Region-by-region layout

| Region | Position and frame intent | Padding, spacing, alignment | Distribution | SwiftUI mapping and behavior |
|---|---|---|---|---|
| Navigation | Inline native bar; each action minimum `44 × 44 pt` | Back leading; title centered; `Batal` trailing only in creation sheet | Edge actions intrinsic; title centered independently | Native toolbar/navigation; Back returns to Quick Add; Batal follows dirty-draft confirmation. |
| Scroll content | Full width between native navigation and save dock | Horizontal `20 pt`; top approx. `12–20 pt`; bottom padding ≥ dock height + `16 pt` | One vertical column | `ScrollView` + leading `LazyVStack`; no nested vertical scroll. |
| Hero | Centered, full available width; content-driven | Thumbnail-to-name `8–12 pt`; badge/value gaps `8–12 pt`; disclaimer after `8–12 pt` | Center-aligned vertical; all text may wrap | Semantic `VStack`; not a large saturated card. |
| Thumbnail | Approx. `64–72 pt` square, aspect fit | Horizontally centered | Fixed proposal width; never stretches | Decorative Bayam thumbnail hidden from VoiceOver because hero combines identity. |
| Food name | Content-driven | Center aligned | Wraps up to sensible width | `.title2.weight(.semibold)`. |
| Urgency badge | Intrinsic pill; minimum tap size not required because noninteractive | Internal horizontal `10–12 pt`, vertical `6–8 pt`; icon/text gap `6 pt` | Centered intrinsic | Tomato-soft background, accessible text/icon; never color-only. |
| Countdown | Full-width text line, intrinsic height | Approx. `8 pt` below badge | Centered | `.largeTitle.bold()` or `.title.bold()` depending Dynamic Type. Exact `Hari ini`. |
| Disclaimer | Width constrained by content column, content-driven | Center aligned; line spacing remains readable | Multiline, never truncated | `.footnote`/`.subheadline`; exact `Ini adalah perkiraan, bukan jaminan keamanan pangan.` |
| Provenance card | Full content width; radius `16 pt` | Internal `16 pt`; row gap/divider approx. `12 pt` | Two rows plus compact provenance label | One `InformationCard`; never card-within-card. |
| Provenance rows | Minimum `44–52 pt`, content-driven | Icon/text gap `10–12 pt`; vertical padding `8–10 pt` | Label flexible leading; value trailing when it fits, otherwise value moves below | `LabeledContent`-style adaptive row. Confidence includes `Sedang`; source may wrap. |
| Interpretation label | Content-driven pill/text, noninteractive | Approx. `8–12 pt` after rows | Leading or centered according to accepted card | Label exact `Interpretasi Fresh`; makes generated values explicit. |
| Inputs heading | Full width, content-driven | Approx. `24 pt` after card; `8–12 pt` before rows | Leading | `.title3.weight(.semibold)`; exact `Berdasarkan`; accessibility heading. |
| Input rows | Full width; minimum approx. `52–60 pt`, content-driven | Internal horizontal `12–16 pt`, vertical `10–12 pt`; divider aligns after icon if grouped | Icon fixed; label column approx. `38–44%`; value flexible/trailing; at narrow widths stack value below label | Reusable adaptive `LabeledInputRow`; raw user text remains primary, normalization supporting. |
| Input icon | Approx. `24–28 pt` symbol area inside optional `28–32 pt` soft circle | Centered vertically/top-aligned when row wraps; gap `10–12 pt` | Fixed | Semantic SF Symbol; hidden if its meaning duplicates row label, never sole source of meaning. |
| Why disclosure | Full width; minimum `52–56 pt`; one quiet surface | Horizontal `16 pt`; chevron gap `8 pt` | Title flexible; chevron intrinsic | `DisclosureGroup`; explanation expands inline below title, not a modal. |
| Adjust action | Full width outline button, approx. `50–54 pt`, radius `14–16 pt` | Top approx. `12–16 pt`; supporting copy `8 pt` below | Centered label | Secondary `Button`; must remain visually weaker than Save. |
| Bottom dock | Anchored outside scroll, surface/material separated from canvas | Top `10–12 pt`; horizontal `20 pt`; bottom native safe area | Error above one full-width primary button | `.safeAreaInset(edge: .bottom)`; button approx. `50–54 pt`; spinner replaces/adds inside label only during visible save work. |

## Canonical input-row content

| Hero/provenance element | Exact content |
|---|---|
| Name and urgency | `Bayam`; `Gunakan hari ini`. |
| Estimate | `Hari ini`; `Perkiraan kualitas terbaik`. |
| Disclaimer | `Ini adalah perkiraan, bukan jaminan keamanan pangan.` |
| Confidence | `Keyakinan estimasi` → `Sedang`. |
| Source | `Sumber panduan` → `Aturan Fresh untuk sayuran berdaun`. |
| Provenance label | `Interpretasi Fresh`. |
| Explanation disclosure | `Mengapa estimasi ini?`. |
| Adjustment | `Sesuaikan estimasi`; `Perbaiki interpretasi atau pilih tanggal sendiri jika hasilnya tidak sesuai.` |
| Primary action | `Simpan bahan`. |

| Row label | Primary value | Supporting interpretation/provenance |
|---|---|---|
| `Kategori oleh Fresh` | `Sayuran berdaun` | Fresh-derived; adjustable. |
| `Penyimpanan` | `Rak atas kulkas` | Interpreted as `Kulkas`. |
| `Kondisi bahan` | `Sudah dicuci` | User text; no inferred ripeness. |
| `Status kemasan` | `Kemasan sudah dibuka` | User text. |
| `Tanggal dibeli` | `12 Agu 2026` | User-selected type/date. |

## Typography

| Element | SwiftUI role | Weight/alignment | Adaptation |
|---|---|---|---|
| Navigation title | `.headline` | Semibold, centered | Native inline navigation. |
| Food name | `.title2` | Semibold, centered | Wraps; never shrinks. |
| Urgency badge | `.subheadline` | Medium/semibold, centered | Remains word-based. |
| Countdown | `.largeTitle` or `.title` | Bold, centered | Scales with Dynamic Type; may use rounded native design. |
| Estimate label | `.subheadline` | Regular, centered | Adjacent to value. |
| Disclaimer | `.footnote` or `.subheadline` | Regular, centered | Never caption-sized if readability suffers. |
| Section title | `.title3` | Semibold, leading | Accessibility heading. |
| Row label | `.subheadline` | Medium, leading | Stays visually separate from value. |
| Row value | `.body`/`.subheadline` | Regular/medium, trailing or leading when stacked | Raw text may wrap fully. |
| Supporting interpretation | `.footnote` | Regular, leading | Explicitly attributed; not critical-only caption. |
| Buttons | `.headline` | Semibold, centered | Full label stays visible. |

## Color, surface, and status tokens

| Role | Light direction | Dark direction | Usage/contrast rule |
|---|---|---|---|
| Canvas | `#F7F5EF` | `#111612` | Main background. |
| Surface | `#FFFFFF` | `#1B211D` | Provenance card, input rows, dock. |
| Primary text | `#18201B` | `#F3F5F1` | Name, countdown, values. |
| Secondary text | `#667068` | `#AAB3AC` | Labels, explanations, disclaimer. |
| Brand | `#1F6B4F` | `#5DBB8E` | Save, Adjust outline, provenance. |
| Brand soft | `#DDEADF` | `#244232` | Icon/provenance backgrounds. |
| Use Today | `#C94B3B` | `#F27868` | Badge/status with text and cue. |
| Needs Review | `#58708A` | `#91A9C1` | Calm unresolved state; never danger red. |
| Divider | `#E4E5DF` | `#343B36` | Row separators/borders. |
| Error | Semantic destructive red | Adaptive destructive red | Save error plus explicit words. |

Normal text targets `4.5:1` contrast. Implement as semantic/adaptive colors and recheck actual rendered Light, Dark, and Increase Contrast output.

## Interaction and persistence

- Back returns to Quick Add with every raw value and draft intact.
- `Mengapa estimasi ini?` expands exact explanation inline: `Sayuran berdaun yang sudah dicuci biasanya perlu diprioritaskan lebih cepat. Kondisi kulkas dan bahan dapat berbeda.`
- `Sesuaikan estimasi` edits interpretation/date inputs; nothing is persisted before a successful Save.
- `Simpan bahan` initiates the first persistence attempt. Only success dismisses the creation sheet and inserts the item into Today/My Food.
- A visible-duration save may show a small progress indicator inside the button and temporarily prevent duplicate submissions; the rest of the content remains visible.

## State adaptations

| State | Required adaptation |
|---|---|
| Needs Review | Slate `Perlu ditinjau`; value `Butuh satu detail lagi`; exact explanation `Fresh belum memahami lokasi penyimpanan “dekat jendela”. Perjelas lokasi agar estimasi lebih berguna.`; primary `Perjelas penyimpanan`; secondary `Simpan tanpa estimasi`. Unknown remains unknown. |
| Save failure | Keep screen/draft; show `Bahan belum tersimpan. Periksa kembali lalu coba lagi.` immediately above dock; primary becomes `Coba simpan lagi`. |
| Smart interpretation unavailable | Preserve raw text; use local matching/rules; show unknown where unresolved; no alarming AI error and no blocked save. |
| Disclosure expanded | Explanation appears inline and pushes following content down; Save dock remains fixed. |
| Edit flow | Primary copy becomes `Simpan perubahan`; success updates existing item instead of inserting another. |
| Dynamic Type | Hero grows; labeled rows stack value below label; buttons/disclaimer never truncate; scroll reaches all content. |
| Dark/Increase Contrast | Use adaptive surfaces/tokens; keep borders, provenance, and selected states distinct. |
| Reduce Motion | Disclosure/state changes use native reduced-motion behavior or short fade; no pulsing urgency. |

## Accessibility annotations

VoiceOver order: Back → `Tinjau estimasi` title → Batal when present → combined hero → disclaimer → confidence/source/provenance → `Berdasarkan` heading → each input row → Why disclosure → Adjust → supporting text → save error when present → Save.

- Combined hero: `Bayam, gunakan hari ini, perkiraan kualitas terbaik hari ini.`
- Read disclaimer as a separate immediately following element; do not hide it as decorative copy.
- Confidence announces the word `Sedang`, not only an icon/color.
- Each input row includes label, raw value, and supporting interpretation only once.
- Decorative thumbnail, checkmarks, and disclosure chevron are hidden as duplicate elements.
- On save failure, announce once and move focus to the error; retain a clear route to retry.
- All interactive controls meet minimum `44 × 44 pt`.

## Compliance matrix

| Requirement from source spec | Met? | Evidence/implementation contract |
|---|---|---|
| Audit before save | Yes | Full feature/provenance contract and explicit Save boundary. |
| Correct Bayam hierarchy/copy | Yes | Hero and canonical row table. |
| Visible food-safety disclaimer | Yes | Hero region and accessibility order. |
| No mysterious AI percentage | Yes | Human-readable confidence/source rows. |
| Raw versus interpreted values distinguished | Yes | Ownership table, `Interpretasi Fresh`, row content. |
| Category reviewed, not entered in Quick Add | Yes | Fresh-derived category row. |
| Needs Review stores unknown | Yes | State table and separate save-without-estimate action. |
| Save errors retain draft | Yes | Persistence and error state contracts. |
| Dynamic Type, VoiceOver, contrast | Yes | Adaptive distribution, reading order, token table. |
| No prohibited feature/safety verdict | Yes | Never show `Safe/unsafe`, probability, health advice, charts, forced input, automatic save, recipes, or nutrition. |

## Review history

1. Canonical available-state v01 established the accepted review-and-save hierarchy.
2. Its small provenance/input icons were accepted as reversible semantic aids that add no data fields.
3. A context-clean reviewer inspected the reconciled Quick Add/Estimate Review handoff and returned `Verdict: No material findings.`

## Assumptions and deviations

- The canonical bitmap represents the available-estimate creation state at default Dynamic Type.
- Needs Review and failures reuse the same shell rather than adding new canonical visual variants.
- Native symbols/material rendering may differ slightly by iOS version; information hierarchy, provenance, contrast, and safety language take priority.

## Decisions needed

None.

## Suggested spec updates

None. This proposal adds implementation measurements without changing the approved product behavior.
