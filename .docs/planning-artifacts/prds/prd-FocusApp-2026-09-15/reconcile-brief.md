---
title: Focus App — Brief/PRD Reconciliation
source_brief: brief-FocusApp-2026-09-15/brief.md
target_prd: prd-FocusApp-2026-09-15/prd.md
created: 2026-09-15
---

# Reconciliation: Brief vs. PRD (Focus App)

Read-only comparison. No source files were edited. Scope: identify what the brief clearly cared about that is now absent from or contradicted by the PRD — not places where the PRD simply made the brief's open questions more specific (that's expected and correct PRD work).

## Method

Read `brief.md` and `prd.md` in full, section by section, cross-referencing:
- Brief: Executive Summary, Problem, Solution, What Makes This Different, Who This Serves, Success Criteria, Scope, Vision
- PRD: Vision, Target User, Glossary, Features (4.1–4.5 / FR-1–FR-12), Non-Goals, MVP Scope, Success Metrics, Open Questions, Assumptions Index

## Gaps Found

### 1. Streak mechanic changed cadence, not just detail (brief scope item vs. PRD reinterpretation)

The brief's Scope section lists **"Daily streaks"** as an in-scope v1 item. The PRD's Streaks feature (FR-11, FR-12) is built entirely around a **Weekly Goal**: "user-configured number of days per week requiring at least one completed Interval," with the Streak counting **consecutive weeks** the goal was met, incrementing/resetting on a weekly boundary.

This isn't the brief's ambiguity being resolved with a specific number (that would be expected PRD work) — it's a different mechanic altogether: "daily streaks" ordinarily implies consecutive-day activity tracking (check in every day, don't break the chain), while the PRD's system is streak-of-weeks, evaluated only at week boundaries, tolerant of skipped days as long as the weekly quota is hit. A user could skip four days in a row under the PRD's design and keep their streak; that would break a literal daily streak. Worth confirming with the user whether this substitution was an intentional decision made during PRD drafting (and if so, it should probably be called out explicitly as a deliberate deviation, the way FR-10's stretch-goal status is flagged) or whether it's an unflagged drift from brief intent.

### 2. Skill Tree's "branching" framing contradicted by PRD's automatic, choice-free unlocks

Brief (Solution section): "A skill tree governs which building types unlock as the city grows, **so progress branches rather than following one fixed path**." This explicitly frames the skill tree as producing divergent progression — implying some form of choice or multiple viable paths, which is the conventional meaning of "skill tree" (vs. a flat unlock ladder).

PRD (4.4 Skill Tree, FR-10): "New Building types unlock automatically as the City reaches milestones — **no active user choice or branch-picking required**." FR-10 consequences: "No user action is required to unlock a new Building type."

The PRD has effectively turned the skill tree into a linear, automatic milestone ladder — the opposite of the "branches rather than one fixed path" quality the brief called out as the specific value of the skill-tree metaphor. This reads as a contradiction rather than a refinement: the brief's stated reason for choosing a skill tree over a simpler unlock system (branching progress) is no longer true of the PRD's design. Flag for the user — either the PRD should restore some branch/choice mechanic, or the brief's framing should be acknowledged as deliberately dropped.

### 3. Competitive differentiation and "why this matters" reasoning entirely absent from PRD

The brief's "What Makes This Different" section carries substantial qualitative reasoning that doesn't survive into the PRD in any form:
- The specific critique of passive/gamified competitors ("A tree that dies quietly when you leave the app doesn't stop you from leaving — it just records that you did")
- The landscape-check finding that no mainstream personal gamified focus app combines active intervention with a progression system, with the closest prior art being a professional time-tracking tool
- The explicit "unfair advantage" framing: built around the actual mechanism of the problem (reflex, not willpower) rather than a bigger reward
- The honest caveat that this isn't a defensible moat — it's a personal project, not a funded product

None of this is expected to appear as an FR (it isn't a requirement), but the PRD has no Background/Context/Competitive-Positioning section at all where this reasoning could live, and the PRD's own section 0 ("read the brief for the why") only partially covers this gap — the differentiation argument is a distinct piece of reasoning from the general problem/solution "why," and a reader relying on the PRD alone loses the competitive rationale for why this product's core mechanic (active intervention) is worth building at all.

### 4. Long-term vision items dropped even where the brief tied them directly to v1 scoping decisions

Brief Executive Summary explicitly pairs the v1 scope decision with the larger vision: "with a phone companion and **a larger vision (multiple city themes, shared cities)** to grow into if it proves itself." The brief's Vision section elaborates: multiple city themes as the answer to novelty decay once the first theme goes stale, and cities that can be private or shared ("turning your own progress into something you'd want to show off").

The PRD's Non-Goals section (section 5) only carries forward two deferred items from the brief's Scope section — phone companion app and cross-platform sync — both of which the brief also listed under "Explicitly out for v1." But the brief's Vision items (multiple themes, private/shared cities) were never listed under "Explicitly out for v1" in the first place; they were framed as the answer to a problem (novelty decay) that the PRD's own Success Metrics still care about (SM-2 is explicitly about avoiding novelty-decay dropoff). The PRD gives no future-facing note that theme variety or sharing is the intended long-term lever against novelty decay — a reader of the PRD alone would not know the product has a planned answer to the exact retention risk SM-2 is tracking.

### 5. Social/pride motivation behind the city metaphor softened to purely functional framing

Brief Executive Summary: progress "is a city, built piece by piece with every completed interval, growing into something you'd want to keep building and **might even want to show a friend**."

PRD Vision (section 1): "every completed interval grows a city, piece by piece, giving the work a shape worth returning to instead of a counter that stops meaning anything after a few weeks."

The PRD keeps the "shape, not a number" reasoning but drops the social/pride dimension (wanting to show someone else) — which in the brief is the emotional seed for the long-term "shared cities" vision item (gap #4 above). This is a minor tone loss on its own, but combined with gap #4 it suggests the social-motivation thread from the brief didn't make it into the PRD at any altitude, even as color/context.

## Non-Gaps (Brief ambiguity correctly resolved by PRD — noted for completeness, not flagged as gaps)

- Progression visualization form: brief left "city-building or similar" as a candidate; PRD locks in a city with Buildings and a Skill Tree in the Glossary — appropriate specification.
- OS-level focus loss as a second drift trigger (FR-2b): not in the brief's explicit scope language but a reasonable, non-contradictory elaboration of "watches for drift"; brief's Open mechanism question (browser extension vs. other) is correctly deferred to Open Questions (PRD section 8, item 2).
- Override behavior (FR-4): brief doesn't specify what happens when a user overrides the block; PRD's "ends the Interval, no City growth, no Streak credit, cannot resume" is a reasonable, non-contradictory specification.
- Counter-metric on override rate (SM-C1): net-new in the PRD, doesn't contradict anything in the brief, and is good practice given the brief's "unfair advantage" framing (product shouldn't become punitive/manipulative) — arguably a faithful extension of brief intent, not a gap.
- Numeric thresholds for building-tier and skill-tree milestones: brief never specified these; correctly left as Open Questions (PRD section 8, item 1).

## Summary Table

| # | Gap | Type | Severity |
|---|-----|------|----------|
| 1 | "Daily streaks" (brief) → weekly-goal streak system (PRD) | Mechanic substitution, not refinement | Medium — changes user-facing behavior |
| 2 | Skill tree "branches rather than one fixed path" (brief) → fully automatic, choice-free unlocks (PRD) | Contradiction | Medium — undercuts brief's stated rationale for the mechanic |
| 3 | Competitive differentiation / "unfair advantage" reasoning | Dropped entirely | Low-Medium — context/rationale loss, not a functional gap |
| 4 | Long-term vision (multi-theme, shared cities) as the answer to novelty decay | Dropped, despite being tied to a still-tracked success metric (SM-2) | Low-Medium |
| 5 | Social/pride motivation ("show a friend") behind the city metaphor | Softened/dropped | Low — tone only |
