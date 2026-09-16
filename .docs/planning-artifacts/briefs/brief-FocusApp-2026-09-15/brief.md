---
title: Focus App
status: draft
created: 2026-09-15
updated: 2026-09-15
---

# Product Brief: Focus App

## Executive Summary

Focus App is a personal productivity tool built on a specific insight: reaching for your phone mid-task isn't a willpower failure, it's a reflex — which means tools that rely on willpower or bigger rewards to fight it are solving the wrong problem. Existing options either passively track whether you stayed focused (and lose their pull once the novelty wears off) or require you to manually remove temptation before the reflex ever kicks in.

This app intervenes instead. During a focus session — Pomodoro-style intervals, customizable to how you actually work — it watches for the moment you drift to a distracting site and steps in immediately: an overlay and a sound, catching the reflex before it becomes a 30-minute scroll session that derails the whole work block. Progress isn't a flat number that stops meaning anything after a few weeks — it's a city, built piece by piece with every completed interval, growing into something you'd want to keep building and might even want to show a friend.

Version one ships on web, targeting students and self-directed learners doing the kind of sustained, unsupervised work where this reflex costs the most — with a phone companion and a larger vision (multiple city themes, shared cities) to grow into if it proves itself.

## The Problem

Reaching for the phone mid-task isn't a conscious decision — it's a reflex. The catch, when it happens, is nearly free: a second's distraction, no real cost. The failure mode is when it isn't caught: a 5-, 10-, or 30-minute scroll session that doesn't just cost those minutes, it derails the entire work session, sometimes pushing the task to another day.

Existing tools address this poorly. Gamified focus apps work at first, but the reward mechanic loses its pull over time — the app gets abandoned, and the phone-reach returns. What actually works is heavy-handed and manual: grayscale mode, Do Not Disturb, and physically moving the phone to another room. Effective, but effortful — it has to be manually reconstructed every single time, and it depends on remembering to do it *before* the reflex kicks in, which is exactly the moment willpower is weakest.

## The Solution

It's a focus app that watches for drift instead of waiting for you to notice it yourself. On the web (v1), it monitors for tab-switches to known-distracting sites while a focus session is active. The moment it catches one, it doesn't rely on you to close the tab yourself — it blocks it with an overlay and plays a sound, an immediate sensory jolt back to what you were doing, before the scroll session has a chance to start.

Focus happens in intervals — classic Pomodoro (25-minute focus, 5-minute break) by default, customizable to fit how you actually work. Completing an interval doesn't just tick a counter — it grows something, like a city being built up piece by piece, giving progress a shape and a story instead of a number going up. A skill tree governs which building types unlock as the city grows, so progress branches rather than following one fixed path.

A phone companion app, planned for later, extends the same drift detection to the device where the reflex actually starts most often.

## What Makes This Different

Other tools are passive or preventive, not active. A tree that dies quietly when you leave the app doesn't stop you from leaving — it just records that you did. Grayscale mode, Do Not Disturb, and physically relocating the phone are preventive: they work, but only if the temptation is removed *before* the reflex kicks in, which requires remembering to set them up every time.

This app intervenes in the moment. Once a session is running, it actively catches the drift as it happens — a tab-switch to a distracting site gets blocked with an overlay and a sound — rather than passively tracking whether you stayed on task. As far as a quick landscape check could find, no mainstream *personal, gamified* focus app does this combination; the closest prior art is a professional time-tracking tool that auto-triggers a blocker on a usage threshold, not a habit-building app with a progression system attached.

This isn't a defensible moat in the startup sense — it's a personal project, not a funded product with a technical edge no one can copy. The "unfair advantage," such as it is, is that it's built around the actual mechanism of the problem (reflex, not willpower) rather than around a bigger reward.

## Who This Serves

Primary user: someone doing sustained, self-motivated work — a student on an assignment, someone learning something on their own — who reflexively reaches for the phone mid-task, has tried gamified and manual tools before, and needs something that intervenes rather than something they have to remember to maintain.

This fits students and self-directed learners in particular: work without an external structure forcing focus on them — no boss standing over your shoulder, no class period ending the distraction for you.

Success isn't "fewer minutes lost to the phone" in isolation — it's a genuinely longer attention span over time. The app should retrain the reflex, not just suppress it session by session.

## Success Criteria

- **Time-before-drift trending upward.** The average length of a focus session before a distracting-site tab-switch is caught should get longer over weeks — direct evidence the reflex is being retrained, not just interrupted.
- **Sustained use, not novelty decay.** Unlike gamified tools that get abandoned once the reward loses its pull, usage should hold or grow over months rather than dropping off after the first few weeks — the specific failure mode this app is built to avoid.

## Scope

**In for v1 (web):**
- Tab-switch drift detection against a blocklist of distracting sites, active during a running focus session
- Overlay block + sound when drift is caught
- Customizable focus/break intervals (Pomodoro defaults: 25/5)
- Visual long-arc progression (city-building or similar) tied to completed intervals
- Daily streaks
- Skill-tree-gated building unlocks for the city (stretch goal — ships in v1 if feasible, otherwise a fast-follow)

**Explicitly out for v1:**
- Phone companion app (the drift detection extended to mobile) — planned, not v1
- Cross-platform progression sync (carrying your city/progress over once the phone app ships) — deferred alongside the phone app itself

## Vision

In 2-3 years, this is a website and a companion phone app with a genuine daily-active userbase — people who open it every day the way they'd check a streak or tend a garden. The city each person builds keeps growing, focus session by focus session, into something substantial rather than a plateau you hit and stop noticing. Multiple city themes give it room to stay fresh as the initial one stops feeling novel — a different answer to the novelty-decay problem than the mechanic itself running dry.

Cities can be kept private or shared — friends can see the city you've built, turning your own progress into something you'd want to show off rather than something only you ever see.

Web and phone stay in sync by then, so the same city grows no matter which device catches the day's focus sessions.
