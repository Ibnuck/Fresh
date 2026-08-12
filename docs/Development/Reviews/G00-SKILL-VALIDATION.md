# G00 Skill Validation

Date: 12 August 2026<br>
Scope: project-local Swift references and Fresh workflow skills<br>
Method: Superpowers test-driven skill authoring with context-clean sub-agents

## Outcome summary

Fresh now has two custom skills only where pressure tests demonstrated a repeatable gap: one for evidence-based code review and one for safe Git/GitHub publication. The broader feature cycle remains in `AGENTS.md` and workflow docs because fresh agents already followed it correctly without another skill.

## Swift skills audit

Installed from Paul Hudson's catalog/repositories:

- `swiftui-pro`
- `swiftdata-pro`
- `swift-concurrency-pro`
- `swift-testing-pro`

Audit result:

- content consists of Markdown guidance, metadata, and icon assets;
- no executable scripts were present;
- the skills were installed project-locally under `.agents/skills`;
- all four passed the official `quick_validate.py` validator;
- their Swift 6.2/version recommendations are advisory; the installed toolchain and project settings remain authoritative.

## `fresh-code-review` RED baseline

Five fresh reviewers inspected the same intentionally flawed Swift fixture without the custom skill. The fixture included:

- a zero-day boundary bug;
- prohibited absolute food-safety wording;
- swallowed SwiftData save failure;
- an unlabeled icon-only action;
- missing visual status tone;
- missing boundary and failure tests despite a green two-test report.

Baseline result:

- reviewers generally found the core bugs;
- severity labels varied (`High/Medium` instead of P0–P3);
- some reviewers combined distinct root causes;
- evidence, contract, and test gap were not always separated;
- reported test success was not always explicitly distinguished from reviewer-run verification.

## `fresh-code-review` GREEN and REFACTOR

The custom skill added:

- strict read-only behavior;
- spec-first observable behavior mapping;
- conditional SwiftUI/SwiftData/concurrency/testing reference use;
- P0–P3 definitions;
- one root cause per finding;
- required Impact, Evidence, Contract, and Test gap fields;
- explicit distinction between reported and reviewer-verified checks;
- exact final verdict.

Five new context-clean reviewers then used the skill. All consistently found the planted material defects, used the required output contract, did not edit files, and ended with `Verdict: Changes required.` The skill passed `quick_validate.py`.

## `fresh-git-workflow` RED baseline

Generic Git advisers were placed under release pressure while G00 was unverified, on unborn `main`, with all files untracked and no authenticated GitHub tooling.

Observed failures included recommendations to:

- create an empty initialization commit;
- create a WIP checkpoint commit;
- push incomplete history;
- open a draft WIP PR before the project quality gate.

These conflict with the user's explicit policy for Fresh.

## `fresh-git-workflow` GREEN and REFACTOR

The custom skill added:

- an exact repository-root boundary;
- a hard no-commit/no-push/no-PR quality gate;
- required fresh clean review before publication;
- Fresh-specific `main`/`dev`/`feature/gXX-name` branches;
- Conventional Commit and PR templates;
- authenticated remote verification;
- no force-push, raw-token workaround, destructive history rewrite, or other-repo operation.

Five context-clean forward tests all returned `Publication blocked`, rejected empty/WIP commits and pushes, and preserved the planned post-gate G00 metadata. The skill passed `quick_validate.py`.

## Feature-cycle skill decision

Three fresh agents were asked to design an end-to-end Fresh goal workflow without a separate feature-cycle skill. Because repo-level `AGENTS.md`, roadmap, workflow, specs, and quality-gate skills were already discoverable, all three independently included:

- outcome summary, spec, and acceptance criteria;
- written implementation plan and TDD;
- native Swift/accessibility checks;
- a different context-clean reviewer after every repair;
- three-cycle root-cause stopping rule;
- no publication before a clean gate;
- branch/commit/PR handoff metadata.

Result: a separate `fresh-feature-cycle` skill would add duplicate injected context without improving observed behavior, so it was intentionally omitted.

## Final validator result

Official `quick_validate.py`: six skills valid, zero failures.

The test fixture and transient validator dependency were kept under `/private/tmp` and are not project artifacts.
