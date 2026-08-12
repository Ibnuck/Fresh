# Personal Agentic Project Playbook

Use this document to bootstrap a new personal software project with an AI coding agent. It is derived from the Fresh project process, but it is intentionally product-agnostic.

## 1. Guiding principle

Start with durable context and feedback loops, not a large agent framework. Add a skill, plugin, sub-agent role, or integration only when it solves a demonstrated recurring problem.

Recommended baseline:

```text
one main coding agent
  + one concise AGENTS.md
  + product/architecture specs
  + written goal plan
  + tests/build/manual checks
  + context-clean read-only reviewer
  + Git quality gate
```

## 2. What to provide at the start

Give the first project chat:

- project idea and target users;
- problem to solve and explicit non-goals;
- platform/framework/toolchain constraints;
- current files/research/reference products;
- desired MVP and quality level;
- privacy, safety, data, offline, and AI constraints;
- how autonomous the agent may be;
- publication policy: branches, commit/push/PR authority;
- whether another chat/tool will produce design images.

If information is uncertain, say so. Unknown is better than an invented requirement.

## 3. Research phase

1. Read all existing Markdown and inspect the repository before proposing structure.
2. Use primary/official sources for frameworks, APIs, agent tools, and technical guidance.
3. Separate stable facts from assumptions and future-facing recommendations.
4. Summarize findings into decisions that actually affect the project.
5. Do not install every interesting tool; audit third-party skills/plugins first.

Useful starting references:

- [OpenAI Codex best practices](https://learn.chatgpt.com/guides/best-practices)
- [AGENTS.md guidance](https://learn.chatgpt.com/docs/agent-configuration/agents-md)
- [Codex skills](https://learn.chatgpt.com/docs/build-skills)
- [Codex sub-agents](https://learn.chatgpt.com/docs/agent-configuration/subagents)
- [Execution plans](https://developers.openai.com/cookbook/articles/codex_exec_plans)
- [AGENTS.md open format](https://agents.md/)

## 4. Brainstorming and ideation

Work from broad to concrete:

1. Restate the problem, user, constraints, and success signal.
2. Propose two or three approaches with real tradeoffs.
3. Choose the simplest approach that meets the requirements.
4. Present design in small reviewable sections:
   - product/MVP boundaries;
   - application architecture/data flow;
   - pages/navigation/states;
   - testing and failure behavior;
   - agentic/Git workflow.
5. Ask for approval of material choices before implementation planning.
6. Write accepted choices to a design spec and decision log.

Do not use brainstorming to endlessly expand features. Every idea should be accepted, rejected, or deferred with a trigger.

## 5. Suggested documentation architecture

```text
AGENTS.md
README.md
.gitignore
.codex/
  config.toml
  agents/reviewer.toml
.agents/skills/
docs/
  PROJECT_JOURNAL.md
  REUSABLE_PROJECT_PLAYBOOK.md
  decisions/
    DECISION_LOG.md
    DECISION_TEMPLATE.md
  Development/
    ARCHITECTURE.md
    WORKFLOW.md
    PRODUCT_ROADMAP.md
    Reviews/
  superpowers/
    specs/
    plans/
ProductSource/Docs/
  DESIGN_SYSTEM.md
  VISUAL_GENERATION_GUIDE.md
  ScreenSpecs/
  VisualReferences/
```

For file-synchronized Xcode projects, exclude documentation folders inside the source group from target membership or keep product docs outside the app source root.

## 6. Goals and outcome summaries

Break the roadmap into goal-sized observable outcomes, not vague phases.

```markdown
## GXX — Goal name

Outcome summary: what the user can actually do when this is complete.

- Branch: feature/gXX-short-name
- In scope: ...
- Out of scope: ...
- Acceptance criteria: observable checks
- Verification: unit/integration/UI/manual/accessibility
```

Prefer a goal that one agent can implement and one reviewer can understand as a coherent diff.

## 7. Implementation loop

```text
outcome and spec
  → written implementation plan
  → failing test for behavior/bug
  → smallest implementation
  → focused tests
  → full applicable verification
  → fresh read-only reviewer
  → validated repair
  → different fresh reviewer
  → clean verdict
  → Git publication gate
```

Rules:

- Never claim a check passed without current observed output.
- Preserve user changes and keep unrelated scope out.
- Validate reviewer feedback technically; do not agree blindly.
- After every repair, use a different context-clean reviewer.
- If the same root cause survives three cycles, stop and analyze before expanding scope.

## 8. Reviewer packet

Give the fresh reviewer only what it needs:

- goal ID and outcome summary;
- spec/acceptance criteria;
- changed files or diff;
- latest verification output;
- explicit exclusions.

The reviewer should be read-only and report prioritized, evidence-based defects with file/line, impact, violated contract, and test gap. It should say `No material findings` when justified rather than inventing feedback.

## 9. When to create a skill

Use test-driven skill authoring:

1. Create a realistic pressure scenario.
2. Run fresh agents without the proposed skill.
3. Record actual repeated failures or inconsistencies.
4. Write the smallest skill that addresses those failures.
5. Run new fresh agents with the skill.
6. Refine only based on observed gaps.

If agents already behave correctly from `AGENTS.md` and docs, do not create a duplicate skill.

Good skill candidates:

- domain-specific code review;
- dangerous/repeatable publication workflow;
- external tool sequence with exact constraints;
- specialized framework rules not reliably known by the model.

## 10. When to use plugins or MCP

Do not install integrations just to appear agentic. Add them when the workflow repeatedly needs an external system such as GitHub PR metadata, Figma files, issue tracking, analytics, database state, or production errors.

Before adding one, answer:

- What recurring task does it remove?
- What data/write authority does it gain?
- Can a local file or existing tool solve it more safely?
- How will success be verified?
- What is the fallback when unavailable?

## 11. UI and image-generation handoff

If another AI creates mockups, give it standalone Markdown:

- product summary and non-goals;
- design intent/tokens/components;
- exact target device/platform;
- one spec per screen with top-to-bottom layout;
- exact copy and consistent example data;
- states, navigation, accessibility, and prohibited elements;
- requested image filenames;
- proposal Markdown template with compliance/deviation tables.

Generated images are proposals. The coding source of truth changes only after material deviations are reviewed and written back into the design system/screen spec.

## 12. Decision memory

Capture a decision when it affects scope, architecture, data/safety/privacy, UX/navigation, platform/dependencies, workflow, Git, or release policy.

Each entry records:

- date/status/scope;
- context and important conversation summary;
- alternatives;
- chosen direction and rationale;
- consequences;
- observable revisit trigger.

Do not store raw chats. Preserve superseded decisions so future agents understand why the project changed.

## 13. Git and publication

Choose publication authority explicitly during bootstrap. For Fresh, the selected policy is owner-managed Git: the agent performs read-only inspection, enforces the quality gate, and provides exact instructions; the owner performs every Git/GitHub mutation. Other projects may choose a different policy, but it must be recorded and unambiguous.

For a simple personal project:

```text
main       stable milestones
dev        accepted goal integration
feature/*  one goal per branch
```

Before any publication handoff or authorized publisher commits/pushes/opens a PR, require:

- complete intended scope/diff inspection;
- no unrelated files or secrets;
- acceptance criteria and current verification pass;
- latest context-clean reviewer has no material findings;
- authenticated remote/repository identity is confirmed.

Default feature PRs to draft. Force-push, destructive history edits, merging, release, and changes to another repository require explicit authority.

## 14. Completion summary

```markdown
## GXX — Goal name

Outcome summary: ...

- What changed: ...
- Verification: exact commands/checks and observed results
- Fresh review: N cycles; final verdict
- Decisions: added/superseded DEC-XXX
- Remaining risk: none known or concrete risk
- Git: branch, commit, push, PR state
```

## 15. Copy-paste prompt for a new project

```text
Read every existing Markdown and inspect the repository before changing files.
Use this playbook as the workflow baseline, but adapt it to the project's actual
platform and risk. Keep the setup suitable for a personal project.

First:
1. summarize current state, unknowns, and constraints;
2. research unstable/technical facts using primary official sources;
3. offer 2–3 product/architecture approaches with tradeoffs;
4. brainstorm and obtain approval for material choices;
5. write a design spec, decision log, outcome-based roadmap, and implementation
   plan before application code;
6. create skills only after a no-skill pressure test demonstrates a repeated gap;
7. implement each goal test-first, verify, then use a new context-clean read-only
   reviewer after every repair until no material findings remain;
8. do not commit, push, or open a PR before the complete goal quality gate;
9. keep important decisions and goal summaries updated in Markdown.

Do not create a website/visual companion unless I explicitly request one. If UI
images will be generated elsewhere, create standalone screen-spec Markdown that
another chat can understand without this conversation.
```

## 16. Keep the playbook alive

Update this playbook only when a project exposes a reusable lesson. Product-specific decisions stay in that project's decision log. Review the playbook after major milestones, not after every small edit.
