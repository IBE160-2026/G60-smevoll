---
title: Focus App
status: final
created: 2026-09-15
updated: 2026-09-15
---

# PRD: Focus App

## 0. Document Purpose

This PRD defines the Focus App for v1 (web). It builds on `brief-FocusApp-2026-09-15/brief.md` — read that for the "why" in full; this document defines the "what," structured as features with nested functional requirements (FR-1 through FR-12), a shared glossary, and MVP scope boundaries.

## 1. Vision

Focus App intervenes on distraction the moment it happens rather than requiring willpower to prevent it. During a focus session, it watches for the reflexive drift to a distracting site and steps in immediately — an overlay and a sound — rather than passively logging that focus was lost. Progress isn't a number: every completed interval grows a city, piece by piece, giving the work a shape worth returning to instead of a counter that stops meaning anything after a few weeks.

v1 ships on web, for students and self-directed learners doing sustained work without external structure forcing focus on them.

## 2. Target User

### 2.1 Jobs To Be Done

- Catch myself before a momentary drift becomes a 30-minute scroll session that derails the whole work block
- Get a visible, cumulative sense that my focus time is actually adding up to something
- Work in a structure (intervals + breaks) without having to build that structure myself every time

### 2.2 Key User Journeys

- **UJ-1.** A student mid-assignment starts a focus interval; when they tab-switch to a distracting site, an overlay blocks it with a sound, pulling them back before the scroll starts, and the completed interval grows their city.

## 3. Glossary

- **Focus Session** — an active period during which drift detection runs, composed of one or more Intervals.
- **Interval** — a single focus/break cycle within a session (default 25 min focus / 5 min break, user-customizable).
- **Drift** — the user's attention leaving focus work during an active Interval, either by switching to a site on the Blocklist within the browser, or by the browser losing OS-level focus to another application entirely.
- **Blocklist** — the set of sites treated as distracting, checked against on every tab-switch during an Interval.
- **Overlay Block** — the intervention shown when Drift is detected: a full-screen overlay plus a sound.
- **City** — the visual, cumulative representation of the user's progress; grows by one or more Buildings per completed Interval.
- **Building** — a discrete unit added to the City on Interval completion; type may be gated by the Skill Tree.
- **Skill Tree** — the branching unlock structure that determines which Building types become available as the City grows.
- **Weekly Goal** — user-configured number of days per week requiring at least one completed Interval.
- **Streak** — count of consecutive weeks in which the user's Weekly Goal was met.

## 4. Features

### 4.1 Drift Detection & Intervention

**Description:** The system monitors tab activity during an active Interval and intervenes the moment the user drifts to a Blocklist site. Realizes UJ-1.

**Functional Requirements:**

#### FR-1: Blocklist configuration

User can view and edit the Blocklist, which ships with a default curated set of known-distracting sites.

**Consequences (testable):**
- A new user has a non-empty default Blocklist on first use, requiring no setup before the feature works.
- Default Blocklist categories are social media and news sites.
- User can add or remove individual sites from the Blocklist at any time.

#### FR-2: Drift detection

System detects Drift via two triggers while a focus Interval is active: (a) tab-switch to a site matching the Blocklist within the browser, or (b) the browser losing OS-level focus to another application entirely.

**Consequences (testable):**
- Trigger (a) fires on tab-switch, not on a polling delay — the Overlay Block (FR-3) appears within the same interaction, not after a noticeable lag.
- Trigger (b) fires immediately when the browser loses OS-level focus.
- Detection is inactive during breaks and when no Interval is running.

#### FR-3: Overlay Block

System shows a full-screen Overlay Block with a sound when Drift is detected; timing depends on the trigger.

**Consequences (testable):**
- For trigger (a) (in-browser tab-switch), the overlay and sound appear immediately, fully obscuring the distracting site's content.
- For trigger (b) (loss of OS-level focus), the sound plays immediately but the Overlay Block is deferred and appears the moment the browser regains focus.
- Sound plays once per Drift event, not repeating.

#### FR-4: Override

User can override the Overlay Block to view the site, which immediately and irreversibly ends the active Interval.

**Consequences (testable):**
- Overriding ends the Interval with no City growth and no Streak credit for that Interval.
- The Interval cannot be resumed after an override — the user must start a new one.

### 4.2 Focus Intervals

**Description:** Structures work into focus/break cycles. Focus Intervals are always user-initiated; breaks start automatically. Realizes UJ-1.

**Functional Requirements:**

#### FR-5: Manual Interval start

User manually starts each focus Interval; the system never starts one on its own.

**Consequences (testable):**
- No focus Interval begins without an explicit user action.

#### FR-6: Customizable Interval lengths

User can configure focus and break durations, defaulting to 25 min focus / 5 min break.

**Consequences (testable):**
- A new user gets a working 25/5 default with no configuration required.
- Changing the duration applies to Intervals started after the change, not one already in progress.

#### FR-7: Automatic break transition

When a focus Interval completes (without override), the break starts automatically.

**Consequences (testable):**
- No user action is required between focus Interval completion and break start.
- The subsequent focus Interval after a break always requires manual start (FR-5).

### 4.3 City Progression

**Description:** Every completed Interval contributes to the City, either placing a small Building immediately or advancing progress toward a larger multi-interval Building. Progress is permanent. Realizes UJ-1.

**Functional Requirements:**

#### FR-8: Building placement

Completing an Interval either places a new small Building immediately or advances a progress bar toward a larger Building requiring multiple completed Intervals.

**Consequences (testable):**
- Every completed Interval visibly changes City state — either a new Building appears, or a progress indicator advances.
- A larger Building only appears once its full multi-interval requirement is met.

#### FR-9: Monotonic progress

City state never decreases regardless of elapsed time or inactivity between sessions.

**Consequences (testable):**
- No Building is ever removed from the City by the system.
- A user returning after weeks away sees their City exactly as they left it, not reset or decayed.

### 4.4 Skill Tree *(stretch goal — ships in v1 if feasible, otherwise fast-follow per brief)*

**Description:** At each City milestone, the user chooses between branch options to unlock new Building types — a real branching tree, not a fixed linear ladder. Extends 4.3.

**Functional Requirements:**

#### FR-10: Branching milestone choice

When the City reaches a milestone, the system presents the user with a choice between branch options; the user picks one to unlock its Building type(s).

**Consequences (testable):**
- At least two branch options are presented at each qualifying milestone.
- The unchosen option(s) remain available to pick at a future milestone — not permanently foregone.
- Only the chosen branch's Building type(s) become available for placement (FR-8) immediately; unchosen branches contribute nothing until picked later.

**Notes:** `[NOTE FOR PM]` Feasibility for v1 vs. fast-follow to be confirmed during architecture/implementation planning — treat as stretch, not committed scope.

### 4.5 Streaks

**Description:** User sets a Weekly Goal (days per week with at least one completed Interval); Streak tracks consecutive weeks that goal is met.

**Functional Requirements:**

#### FR-11: Weekly Goal configuration

User can set a Weekly Goal: the number of days per week requiring at least one completed Interval.

**Consequences (testable):**
- Goal is configurable at any time; changes apply from the next week boundary, not retroactively to the current week.

#### FR-12: Streak tracking

System increments Streak by one at the end of any week where the Weekly Goal was met, and resets Streak to zero at the end of any week where it was not met.

**Consequences (testable):**
- A week exactly meeting the goal (not exceeding it) still counts.
- Streak reset is visible to the user, not silent.

## 5. Non-Goals (Explicit)

- Phone/mobile app — planned for a later phase, not v1
- Cross-platform progression sync — deferred alongside the phone app
- Auto-starting focus Intervals — the system never initiates a session; the user always does (FR-5)
- Monetization of any kind
- Leaderboards or competitive ranking between users — considered and explicitly rejected (retention risk)
- Repurposing time-tracking data as a workplace/project timesheet tool — a different product for a different user, not this app's direction

## 6. MVP Scope

### 6.1 In Scope

- Drift detection and Overlay Block intervention (FR-1–FR-4)
- Configurable focus/break Intervals (FR-5–FR-7)
- City progression (FR-8–FR-9)
- Skill Tree Building unlocks (FR-10) — stretch, ships if feasible
- Weekly-Goal Streaks (FR-11–FR-12)

### 6.2 Out of Scope for MVP

- Everything listed under Non-Goals above

## 7. Success Metrics

**Primary**
- **SM-1**: Average focus-session length before a Drift is caught, trending upward over weeks. Validates FR-2, FR-3.

**Secondary**
- **SM-2**: Weekly active usage sustained or growing over months, not dropping off after the first few weeks. Validates FR-8, FR-11, FR-12.

**Counter-metrics (do not optimize)**
- **SM-C1**: Override rate (FR-4) should not be optimized toward zero by making override artificially punishing beyond ending the Interval — the goal is honest catch-and-return behavior, not trapping the user. Counterbalances SM-1.

## 8. Open Questions

1. Numeric threshold for a "larger" Building's multi-interval progress bar, and how many completed Intervals unlock each Skill Tree milestone (FR-8, FR-10) — deferred.
2. Technical mechanism for OS-level focus-loss detection and in-browser drift detection (browser extension vs. other approach) — deferred to architecture.

## 9. Assumptions Index

None — Coaching path was used throughout, and every decision in this document was confirmed directly with the user rather than inferred.
