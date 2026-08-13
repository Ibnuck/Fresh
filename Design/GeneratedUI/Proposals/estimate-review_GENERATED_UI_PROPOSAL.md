---
proposal_for_screen: estimate-review
proposal_version: 1
generator: Codex image generation
generated_at: 2026-08-13
source_spec_version: 2
approval_status: canonical-approved
---

# Generated UI Proposal — Estimate Review

## Canonical output

| State | Image | Role |
|---|---|---|
| Estimate available — new Bayam draft | `../Screens/estimate-review_available_light_v01.png` | **Canonical** review-and-save hierarchy; context-clean reviewer returned no material findings. |

The generated image adds small semantic icons for provenance and each labeled input row. These are accepted native/reversible affordances: they improve scanning without changing information ownership or adding fields.

Needs Review, save error, Dark Mode, disclosure expansion, and Dynamic Type remain implementation states defined below and in the source spec.

## Feature and information contract

Estimate Review is the boundary between an unsaved Quick Add draft and a persisted food. It must let the user audit the estimate before choosing `Simpan bahan`.

| Displayed information | Ownership/meaning |
|---|---|
| Name, raw storage, condition, package, reference date | Entered by the user and preserved exactly. |
| Category and normalized storage/condition/package tags | `Interpretasi Fresh`; derived through local matching and optional Foundation Model. |
| Urgency/countdown | Deterministic verified rule engine result, not Foundation Model world knowledge. |
| Confidence/source | Human-readable explanation of rule/input completeness, never a mysterious AI percentage. |
| Disclaimer | Estimate is not a food-safety guarantee. |

Category is shown here because the user did not enter it in Quick Add. A clearly wrong interpretation can be adjusted. Unstated ripeness, package state, condition, storage, or date remains unknown.

## Canonical hierarchy

1. Inline navigation `Tinjau estimasi`, back, and optional sheet `Batal`.
2. Bayam thumbnail, name, `Gunakan hari ini`, countdown `Hari ini`, estimate label, and visible disclaimer.
3. Compact confidence/source card with `Interpretasi Fresh` provenance.
4. `Berdasarkan` rows that distinguish raw text and normalization.
5. `Mengapa estimasi ini?` disclosure and `Sesuaikan estimasi` secondary action.
6. Keyboard-independent safe-area primary action `Simpan bahan`.

## Interaction and persistence

- `Simpan bahan` performs the first persistence attempt; success dismisses the creation sheet and inserts the item into Today/My Food.
- Persistence failure retains the draft/screen and shows `Bahan belum tersimpan. Periksa kembali lalu coba lagi.` with `Coba simpan lagi`.
- Back returns to Quick Add without losing the draft. `Batal` follows the discard-confirmation policy.
- `Sesuaikan estimasi` changes interpretation/date inputs; it does not mutate saved data before save succeeds.
- `Mengapa estimasi ini?` expands a short rule explanation inline.

## Alternate implementation states

- **Needs Review:** `Perlu ditinjau`, `Butuh satu detail lagi`, one specific unresolved input, `Perjelas penyimpanan`, and `Simpan tanpa estimasi`. Saving without estimate is allowed and stores unknown; never invent a countdown.
- **Smart interpretation unavailable:** preserve raw text; use local matching/rules where possible; do not block the flow or display an alarming AI error.
- **Dynamic Type:** hero and labeled rows stack/grow; disclaimer and CTA never truncate.
- **Dark/Increase Contrast:** adaptive semantic colors with normal text at least `4.5:1`.

## Scope guardrails

No safe/unsafe verdict, exact AI probability, health advice, scientific chart, automatic save, forced input, recipe, nutrition, or long citation page.
