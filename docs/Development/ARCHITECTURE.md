# Fresh Architecture

## Shape

```text
SwiftUI View
  → @Observable feature model
  → narrow service/repository boundary
  → SwiftData + deterministic freshness rules
```

Folders grow feature-first: `App`, `Features`, `Core`, `DesignSystem`, and `Resources`. Do not create all empty folders upfront; add them with the first goal that owns real files.

## Boundaries

- Views render state and send user intent; they do not calculate freshness.
- Feature models coordinate one screen/flow and expose testable states.
- Core owns domain models, persistence, rules, notifications, and optional intelligence adapters.
- DesignSystem owns reusable visual tokens/components without business rules.
- Foundation Models may interpret input but never generate food-safety facts or block core functionality.
- SwiftData model/context values do not cross actor boundaries; use stable identifiers and refetch when needed.

## Error policy

- Preserve user drafts after recoverable errors.
- A failed save is visible and retryable.
- Notification failure does not roll back an item that saved successfully.
- Unknown data stays unknown; it is never replaced with a convenient false default.
- If an estimate cannot be justified, use `Needs Review` or a user-provided custom estimate.

## Testing seams

Extract deterministic domain rules first. Introduce protocols only for external/system boundaries or failure injection that tests genuinely require. Use Swift Testing for unit/integration and XCTest for UI tests.
