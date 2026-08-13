---
proposal_for_screen: my-food
proposal_version: 2
generator: Codex image generation
generated_at: 2026-08-13
source_spec_version: 2
approval_status: canonical-approved
---

# Generated UI Proposal — My Food

## Outputs

| State | Appearance | Image file/path | Status |
|---|---|---|---|
| Populated | Light | `../Screens/my-food_populated_light_v04.png` | **Canonical**; fresh reviewer returned no material findings. |
| Populated, superseded | Light | `../Screens/my-food_populated_light_v01.png`–`v03.png` | Review/revision history; do not implement. |
| Search empty | Light | `../Screens/my-food_search-empty_light_v01.png` | Supplementary state reference; fresh reviewer returned no material findings. |
| Dynamic Type | Light | Not generated | Defined in spec and verified during SwiftUI implementation. |

## Intended hierarchy

1. Large title `Makananku` and Settings.
2. Native search field `Cari bahan`.
3. Storage filters `Semua`, `Kulkas`, `Freezer`, `Dapur`.
4. Stable urgency sections: `Gunakan hari ini`, `Segera gunakan`, `Masih fresh`, `Perlu ditinjau`.
5. Exactly three app-level destinations with `Makananku` selected.

## Runtime structure

```text
NavigationStack
├── searchable("Cari bahan")
├── ScrollView(.horizontal)
│   └── storageFilterChips
├── List / LazyVStack
│   ├── urgencySection(Bayam)
│   ├── urgencySection(Susu segar)
│   ├── urgencySection(Tempe)
│   └── urgencySection(Alpukat)
├── toolbar(settings)
└── app-level bottom navigation
```

Rows are content-driven with a `72 pt` default minimum, adaptive wrapping, a decorative `48–56 pt` thumbnail, combined VoiceOver content, and a full-row navigation target. Search is local and appears only on My Food. Filter chips remain horizontally scrollable and announce selection.

## Reusable transparent assets

- `food_thumbnail_bayam_transparent.png`
- `food_thumbnail_susu_transparent.png`
- `food_thumbnail_tempe_transparent.png`
- `food_thumbnail_alpukat_transparent.png`

These are decorative row thumbnails scoped to approximately `48–64 pt`, not detail heroes. The image-generation chroma background is not part of the delivered assets; each listed PNG has an alpha channel and transparent outer background.

`food_thumbnail_tempe_transparent.png` was repaired after the original chroma-removal pass incorrectly removed cream-white pixels inside the tempeh texture. The runtime asset now uses a conservative border-connected magenta mask: only the saturated chroma region connected to the outer canvas becomes transparent, while the complete soybean/mycelium texture remains opaque. Validate this asset at its intended `48–64 pt` row size on both Light and Dark surfaces; do not crop the Tempe image embedded in an older screen bitmap.

## Review notes

The first populated draft placed the Alpukat row beneath the bottom navigation and omitted the complete safe-area shell. After targeted spacing/safe-area repairs, v04 shows the full final row, a clear canvas separation, the rounded native tab surface, and home indicator. A different context-clean reviewer compared v04 with the specification, proposal, approved Today shell, and superseded baseline, then returned `Verdict: No material findings.`

The canonical bitmap predates the corrected Tempe alpha matte. Treat its layout as authoritative but supply the row from the repaired standalone runtime asset documented above.

Judge screens at normal iPhone viewing size and thumbnails at their intended row size. Material blockers include clipped content behind the tab bar, wrong exact copy/data, inaccessible ordinary text, broken navigation hierarchy, or prohibited feature drift. Microscopic source irregularities invisible at intended size are not blockers.
