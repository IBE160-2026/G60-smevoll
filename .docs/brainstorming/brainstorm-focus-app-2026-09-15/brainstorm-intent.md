# Brainstorm Intent: Focus App

Source: brainstorming session `brainstorm-focus-app-2026-09-15` (Laddering, SCAMPER, Six Thinking Hats, Lotus Blossom). This document distills that session into input for downstream product planning. Scope: personal focus/distraction-blocking app only.

## What Is Being Built

A personal focus/productivity app. Surface pitch: a timer that blocks notifications so the user can concentrate, combined with time logging per task so the user "levels up." That surface pitch is a tactic, not the product's reason for existing (see below).

## Why (Real Underlying Need)

Laddering traced the surface pitch down to its root need:

fewer distractions -> true focus (retraining the brain out of reflexively reaching for the phone) -> self-trust (being able to trust yourself to actually get things done, reclaiming time from social media/screen time) -> **actually reaching the goals you set for yourself**.

The notification-blocking timer is one tactic in service of that root need, not the product's core value. Two supporting ideas sit at this root level: a mechanism to interrupt the brain's reach for short-term dopamine hits, and a long-view retrospective that lets the user look back weeks/months/years and see how far they've come.

A critical behavioral fact (Six Thinking Hats, White Hat) grounds the design: the phone-reach is **reflexive and unconscious, not a conscious willpower failure**. This produces a specific risk loop (Red Hat -> Black Hat): the user catches themselves reflexively reaching for the phone -> feels guilt/self-annoyance -> scrolling still feels better in the moment than the app's reward -> the app loses to instant gratification and gets abandoned. Most reward-based ideas (streaks, town-building, skill trees) fight this loop by offering a bigger dopamine hit, which does not address the reflexive, unconscious root of the behavior.

## Core Spine (What the Session Converged On)

1. **Automatic intervention on reflexive distraction ("Reverse" idea)** — instead of requiring the user to consciously start a focus session, the app detects distraction/drift and locks the user into focus mode automatically. This is the one idea that addresses the reflexive nature of the phone-reach directly, rather than trying to out-compete it with willpower or bigger rewards. This is the key differentiating mechanic.
2. **Visual long-arc progression, not a flat number** — progression should be represented as a visual, cumulative representation of goal-reaching over time (mirroring the "long-view retrospective" need from Laddering), not a flat XP counter. SCAMPER's Eliminate step proposed cutting gamification/leveling entirely, but every other technique (SCAMPER Substitute, Green Hat, Lotus Blossom) independently reached for richer, non-numeric progression. Conclusion: the flat XP *number* was the real target for elimination — the concept of progression itself should stay, just not as a flat number.

Progression-visualization candidates surfaced (not yet chosen between — see Open Questions):
- Skill tree (branching progress instead of a single number)
- City/town building (start on empty plains, build up as focus time accumulates)
- A large cube/block slowly mined away
- A hiking trail / journey
- A leveled character
- Driving around a planet / generic game-like progression / per-task unlocks / achievements

## Supporting Ideas Worth Keeping Visible

- **Calendar integration**: merge with a calendar app to auto-schedule focus sessions instead of manually starting a timer.
- **Duolingo-style daily streaks** applied to daily focus sessions.
- **Cross-platform**: web browser and phone.
- **Simplicity**: the app should be simple to use.
- **Monetization**: stated as a future consideration; not detailed further in the session.

## Open Questions / Forks Parked

- **Progression visualization form is undecided.** Multiple strong candidates exist (skill tree, city-building, mined cube, hiking trail, leveled character) but none was chosen. Downstream planning should pick or shortlist one rather than treat this as settled.
- **Session length/rigidity is unresolved.** SCAMPER's Modify step proposed the extreme of forced 5-minute micro-sessions instead of long focus blocks; this was raised but not evaluated or resolved against the auto-detect/lock ("Reverse") mechanic.
- **Out of scope for this doc**: the "Put to Other Use" idea (repurposing time-logging data into a workplace timesheet tool for switching between project timers) was raised and explicitly rejected as scope for this intent document — it targets a different user (employee time-reporting) and is a separate potential product fork, not part of v1 for this personal focus app.
