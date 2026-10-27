---
title: Focus App
status: draft
created: 2026-09-15
updated: 2026-10-27
---

# Product Brief: Focus App

## Executive Summary

Focus App is a personal productivity tool built on a specific insight: reaching for a distraction mid-task isn't a willpower failure, it's a reflex — which means tools that rely on willpower or bigger rewards to fight it are solving the wrong problem. Existing options either passively track whether you stayed focused (and lose their pull once the novelty wears off) or require you to manually remove temptation before the reflex ever kicks in.

This app intervenes instead. During a focus session — Pomodoro-style intervals, customizable to how you actually work — it notices the moment you open a distracting site and steps in immediately with a warning window and a 10-second countdown, catching the reflex before it becomes a 30-minute scroll session that derails the whole work block. Progress isn't a pile of coins and badges — it's a city, built one building at a time from the focus minutes you complete.

Version one is a Chrome extension for desktop, targeting students and self-directed learners doing the kind of sustained, unsupervised work where this reflex costs the most. A phone companion is a later step, not part of v1.

## The Problem

Reaching for a distraction mid-task isn't a conscious decision — it's a reflex. The catch, when it happens, is nearly free: a second's distraction, no real cost. The failure mode is when it isn't caught: a 5-, 10-, or 30-minute scroll session that doesn't just cost those minutes, it derails the entire work session, sometimes pushing the task to another day.

Existing tools address this poorly. Gamified focus apps work at first, but the reward mechanic loses its pull over time — and the apps themselves tend to grow heavy, with many steps before a session starts, several currencies to keep track of, slow startup and crashes. The app gets abandoned, and the reflex returns. What actually works is heavy-handed and manual: grayscale mode, Do Not Disturb, and physically moving the phone to another room. Effective, but effortful — it has to be manually reconstructed every single time, and it depends on remembering to do it *before* the reflex kicks in, which is exactly the moment willpower is weakest.

## The Solution

Focus App is a Chrome extension (Manifest V3). Everything the user works with — starting a session, the running timer, the city — lives in one extension tab. A plain web page cannot see or interrupt other tabs, which is why v1 is an extension rather than a website.

**A session.** The user starts a focus session (classic Pomodoro 25/5 by default, customizable). While it runs, the extension checks each site the user opens against a blocklist. The extension ships with a default blocklist (for example YouTube, TikTok, Instagram, Reddit) that the user can edit. Outside a session, nothing is blocked.

**The catch.** When the user opens a blocklisted site during a session, a warning window appears over the page, with the page still visible behind it, and a 10-second countdown starts. If the user leaves the site within 10 seconds, the session continues. If they stay past 10 seconds, or close the warning window, the session is aborted and earns nothing. The rule is deliberately strict: the reflex should cost something.

**The city.** Focus minutes are the only progress unit. The user chooses which building to construct next from five building types; larger buildings need more focus minutes. Each completed session adds its minutes to the building under construction, and the next building starts when it is finished. The same type can be built many times, but the user cannot switch buildings mid-construction.

**Streaks.** A day counts toward the streak when at least one session is completed (calendar day, local time). A day without one resets the streak to zero. The streak is shown as a number; it does not affect the city.

**Privacy.** The extension only checks visited sites against the blocklist during an active session. Browsing history is never stored or sent anywhere. App data — sessions, city, streak, blocklist and settings — is stored locally in the browser. There is no login and no server.

## What Makes This Different

Site blockers like StayFocusd and LeechBlock block outright, with no progress to earn; Forest's browser extension pairs a blocklist with a growing tree. Focus App sits between them: a 10-second warning gives the user a chance to turn back, but staying — or dismissing the warning — costs the whole session. Progress is one thing only, focus minutes, spent on a city the user chooses how to build.

It is also deliberately light. Focus App aims for the opposite of the heavy gamified apps: few clicks to start, no currencies, no store.

This isn't a defensible moat — it's a personal project, and the pieces exist elsewhere. The case for it is the combination, built around the actual mechanism of the problem (reflex, not willpower), and kept simple enough to keep using.

## Who This Serves

Primary user: someone doing sustained, self-motivated work — a student on an assignment, someone learning something on their own — who reflexively drifts to distracting sites mid-task, has tried gamified and manual tools before, and needs something that intervenes rather than something they have to remember to maintain.

This fits students and self-directed learners in particular: work without an external structure forcing focus on them — no boss standing over your shoulder, no class period ending the distraction for you.

## Success Criteria

v1 succeeds when each of these can be demonstrated:

**Blocking**
- When the user opens a blocklisted site during an active session, a warning window appears over the page within 1 second, with a visible 10-second countdown.
- If the user leaves the site within 10 seconds, the session continues uninterrupted.
- If the user stays past 10 seconds, or closes the warning window, the session is aborted and adds no focus minutes.
- Outside an active session, blocklisted sites open normally.
- The extension ships with a default blocklist, and the user can add and remove sites.

**Sessions, city and streaks**
- A session completes when its set focus time runs out; its minutes are added to the building under construction.
- A building is finished when its required focus minutes are reached; the user then chooses the next one.
- A day with at least one completed session extends the streak; a day without one resets it to zero.

**Lightweight**
- With the default interval, a session can be started in at most two clicks from the extension icon.
- Focus minutes are the only progress unit — no coins, gems or other currencies.
- The extension tab opens and is usable within 1 second.
- Progress survives closing and reopening the browser.

The blocking criteria are verified with a documented manual test plan; session, city and streak rules are covered by unit tests.

## Scope

**In for v1 (Chrome extension):**
- One extension tab with session start, timer and city view
- Customizable focus/break intervals (Pomodoro defaults: 25/5)
- Default blocklist, editable by the user
- Warning window with 10-second countdown on blocklisted sites during a session; abort rule as above
- City with five building types of different build times, chosen by the user
- Daily streak, shown as a number
- Local storage only — no login, no server
- Skill-tree-gated building unlocks (stretch goal — ships in v1 if feasible, otherwise a fast-follow)

**Explicitly out for v1:**
- Other browsers than Chrome
- Phone companion app — planned, not v1
- Cross-device progression sync — deferred alongside the phone app
- Accounts, cloud backup or sharing

## Open Questions and Next Steps

- **Technical spike before the PRD.** A minimal extension that shows the warning window on one blocked site, to confirm the core works — the group has not built a browser extension before.
- **Sound with the warning.** Whether a sound helps or is too irritating will be tested in the spike before it is decided.

## Vision

In 2–3 years, this is a browser extension and a companion phone app with a genuine daily-active userbase — people who open it every day the way they'd check a streak or tend a garden. The city each person builds keeps growing, focus session by focus session, into something substantial rather than a plateau you hit and stop noticing. Multiple city themes give it room to stay fresh as the initial one stops feeling novel.

Cities can be kept private or shared — friends can see the city you've built, turning your own progress into something you'd want to show off rather than something only you ever see. Desktop and phone stay in sync by then, so the same city grows no matter which device catches the day's focus sessions.

The long-term measures of success live here: time-before-drift trending upward over weeks — evidence the reflex is being retrained, not just interrupted — and use that holds over months rather than dropping off after the novelty wears off.
