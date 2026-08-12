# Fresh Decision Memory

This folder preserves project reasoning without preserving entire chat transcripts.

## What belongs here

Record a decision when it changes or constrains:

- product goals, MVP scope, or roadmap order;
- architecture, data ownership, persistence, privacy, safety, or AI boundaries;
- important navigation, interaction, visual direction, or sensitive copy;
- supported platform/toolchain/dependencies;
- agent workflow, testing, review, stopping conditions, Git, or release policy;
- selection or rejection of a meaningful alternative that future work may question.

Do not record routine naming, small reversible refactors, or every conversational message.

## Workflow

1. During brainstorming, identify the decision and alternatives.
2. Before or alongside dependent implementation, add an entry to `DECISION_LOG.md` using `DECISION_TEMPLATE.md`.
3. Link the relevant spec/plan/research when available.
4. If changed later, keep the old record, mark it `superseded`, and link the replacement decision.
5. During goal completion, mention newly added or superseded decision IDs.

## Status values

- `proposed`: written but not accepted.
- `accepted`: current source of truth.
- `superseded`: replaced by a newer entry.
- `rejected`: considered and intentionally not chosen.
- `deferred`: valuable but postponed until a trigger occurs.
