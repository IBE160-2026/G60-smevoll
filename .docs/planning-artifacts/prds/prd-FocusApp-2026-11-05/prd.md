---
title: Focus App
status: draft
created: 2026-11-05
updated: 2026-11-10
---

# PRD: Focus App

## 0. Document Purpose

This PRD turns the revised product brief (`.docs/planning-artifacts/briefs/brief-FocusApp-2026-09-15/brief.md`, updated 2026-10-27) into testable requirements for v1. It is written for the project group, the teacher and the examiner, and for the next BMAD steps (UX, architecture, epics). Terms in §3 Glossary are used exactly as defined. Features are grouped in §4, with requirements numbered FR-1 to FR-N across the whole document. Deliberate deviations from the brief are listed in §1.1 so the examiner can trace each one. The decisions behind this PRD are logged in `.memlog.md` in the same folder.

## 1. Vision

Focus App is a Chrome extension for people who drift to distracting sites by reflex while doing concentrated work. During a session it watches for blocklisted sites. When one opens, a warning window gives the user 10 seconds to turn back before the session is lost. Every completed session adds focus minutes to a city that the user builds one building at a time.

The product is built on one idea from the brief: drifting is a reflex, not a lack of willpower. So the app catches the reflex at the moment it happens, instead of relying on the user to remember to lock things down beforehand. It stays deliberately light: a session starts in two clicks, focus minutes are the only progress unit, and there are no accounts, currencies or store.

### 1.1 Deviations from the Brief

| # | Brief says | PRD says | Why |
|---|---|---|---|
| D-1 | Target user is students and self-directed learners | Anyone doing concentrated work at a PC | The reflex is the same in a job, at school and in spare-time learning |
| D-2 | Closing the warning window aborts the session | The window has no close control; the "Abort session" button aborts | Makes the cost explicit and gives one clear way out |
| D-3 | Outside a session, nothing is blocked | After a session ends, blocklisted sites show a reminder window, with no penalty, until the user chooses a new session or a break | A session that ends unnoticed should not leave the user drifting without a nudge |
| D-4 | Technical spike before the PRD | PRD written before the spike | The group chose to start the PRD now; blocking feasibility and the warning sound remain open (§8) |

## 2. Target User

Anyone doing concentrated work at a PC, whether for a job, for school or to learn something in their spare time, who drifts to distracting sites by reflex (D-1).

### 2.1 Key User Journeys

**UJ-1. Ida finishes a focus session and sees her city grow.**
- **Persona + context:** Ida is teaching herself programming in her spare time. It takes concentration, and she knows she drifts to distracting sites without deciding to.
- **Entry state:** At her PC, working in Chrome or in another program such as VS Code. The extension is installed. No login or setup is needed (see UJ-4).
- **Path:**
  1. Ida starts a session from the extension, with the length she has chosen.
  2. A timer counts down while she works, shown the way she has chosen: full screen on a screen of its own, a small window in the corner of the browser, or not at all.
  3. By reflex, she opens a blocklisted site. A warning window appears over the page, with a 10-second countdown blinking red and a text telling her to leave the site to keep the session.
  4. She leaves the site within the 10 seconds, and the session continues.
- **Climax:** The timer reaches zero. A visual cue tells her she has done something good, a sound plays if she has turned it on, and she sees how much the progress bar of the building under construction has grown.
- **Resolution:** She chooses between starting a new session and starting a break, during which she can visit any site. The choice waits until she makes it.
- **Edge case:** With the timer hidden and the sound off, nothing interrupts Ida when the session ends. This is deliberate: she is probably deep in her work, and a notice could break her focus. The minutes are added anyway, and she sees the result the next time she opens the extension. Minutes she works after the timer reaches zero do not count. If she opens a blocklisted site before choosing between a new session and a break, a reminder window appears. It says the session is finished, has no countdown and puts nothing at risk, and offers the same choice: a break leaves the site open, and a new session gives the normal 10-second warning. The reminder comes back on blocklisted sites until she has chosen.

**UJ-2. Ida stays on YouTube and loses the session.**
- **Persona + context:** Ida again, on a tired day, in the middle of a session.
- **Entry state:** A session is running, and she has just opened YouTube, which is on the blocklist.
- **Path:**
  1. The warning window appears over the page, with the 10-second countdown blinking red, a text telling her to leave the site to keep the session, and an "Abort session" button.
  2. She stays on the site until the countdown reaches zero. Pressing the button has the same result, immediately.
- **Climax:** The session is aborted and adds no focus minutes. The window stays on screen and asks, in a neutral tone, whether she wants to start a new session.
- **Resolution:** If she declines, the window closes and YouTube is open as normal. She can start a new session later from the extension.
- **Edge case:** If she accepts while still on YouTube, the warning window appears again with a new 10-second countdown, because she is still on a blocklisted site.

**UJ-3. Ida finishes a building and sees her city grow.**
- **Persona + context:** Ida some weeks later, with a few buildings already in her city.
- **Entry state:** A session is running, and the building under construction is close to its required focus minutes.
- **Path:**
  1. The timer reaches zero, and the session's minutes bring the building up to its required focus minutes.
  2. She opens the extension.
- **Climax:** The building is finished. She sees it standing in the city, and the city has grown.
- **Resolution:** She picks the next building from a menu of the five building types, Type 1 to Type 5, which need 1, 2, 3, 4 and 5 hours of focus minutes (names and look to be decided later). If she does not pick one, the same type as last time is built.
- **Edge cases:**
  - She can change her pick until the next session starts. The building is then locked, as the brief does not allow switching mid-construction.
  - Minutes left over when a building is finished go to the next building.
  - Before her first building there is no "last time", so Type 1 is preselected and she can start a session without choosing.

**UJ-4. Ida installs the extension and starts her first session.**
- **Persona + context:** Ida on the day she installs the extension, wanting to try it straight away.
- **Entry state:** The extension has just been installed. Nothing is set up, and she has no focus minutes.
- **Path:**
  1. She opens the extension and sees an empty city with a Type 1 building under construction and an empty progress bar.
  2. She starts a session without setting anything up. The defaults apply: 25-minute sessions with 5-minute breaks, a blocklist with YouTube, TikTok, Instagram and Reddit, the timer as a small window in the corner of the browser, and the end-of-session sound turned on.
- **Climax:** The first session ends, the sound plays, and the progress bar of her first building moves for the first time.
- **Resolution:** She later adjusts the blocklist, intervals, timer display and sound to suit how she works.

## 3. Glossary

- **Session** — A focus period with a set length, started by the user. It is *running*, *paused*, *completed* or *aborted*. Only one session exists at a time.
- **Focus minutes** — The only progress unit. A completed session adds its full set length in focus minutes; an aborted session adds none.
- **Break** — A period after a session, chosen by the user, during which nothing is blocked.
- **End-of-session choice** — The choice between a new session and a break, offered when a session is completed. It waits until the user makes it.
- **Blocklist** — The user's list of sites that trigger the warning window during a session.
- **Warning window** — The window shown over a blocklisted site during a running session, with a 10-second countdown and an "Abort session" button.
- **Reminder window** — The window shown over a blocklisted site after a session is completed and before the end-of-session choice is made. It has no countdown and no penalty.
- **Timer display** — How the running session's timer is shown: *full screen*, *corner* (a small window in the corner of the browser) or *hidden*.
- **Building type** — One of Type 1 to Type 5, requiring 60, 120, 180, 240 and 300 focus minutes.
- **Building under construction** — The single building that receives focus minutes. Its type is locked once a session starts.
- **City** — All finished buildings, plus the building under construction.
- **Streak** — The number of consecutive calendar days, in local time, with at least one completed session.
- **Demo mode** — A setting in which 1 real second counts as 1 focus minute, used to demonstrate the app. It uses the demo city.
- **Demo city** — A separate city, with its own progress, used only in demo mode.

## 4. Features

### 4.1 Focus Sessions

**Description:** The user starts a session from the extension in at most two clicks. The timer is shown as the user has chosen. When the session is completed, the user sees the result and makes the end-of-session choice. If Chrome closes, crashes or the PC sleeps, the session pauses and resumes automatically when Chrome opens again. Realizes UJ-1, UJ-4.

#### FR-1: Start a session
The user can start a session with the current session length from the extension. Realizes UJ-1, UJ-4.
- With default settings, a session starts in at most two clicks from the extension icon.
- No setup is required before the first session.
- A session cannot be started while another session is running or paused.

#### FR-2: Set session and break lengths
The user can set the session length and the break length. Defaults are 25 and 5 minutes. Realizes UJ-4.
- A changed length applies from the next session started.
- [ASSUMPTION: lengths are whole minutes between 1 and 120.]

#### FR-3: Choose the timer display
The user can choose between the full screen, corner and hidden timer displays. Default is corner. Realizes UJ-1.
- Full screen shows the timer filling a browser window, intended for a separate screen.
- Corner shows a small timer window in a corner of the browser. It is not shown over other programs.
- Hidden shows no timer while the session runs.

#### FR-4: Complete a session
When the timer of a running session reaches zero, the session is completed and its full length is added as focus minutes to the building under construction. Realizes UJ-1.
- The minutes are added whether or not the user is watching.
- Minutes after the timer reaches zero are not counted.
- A visual cue and the progress bar's growth are shown the next time the extension is visible.

#### FR-5: End-of-session sound
The user can turn the end-of-session sound on or off. Default is on. Realizes UJ-1, UJ-4.
- With the sound off and the timer hidden, nothing signals the end of the session.

#### FR-6: End-of-session choice
After a session is completed, the user chooses between a new session and a break. Realizes UJ-1.
- The choice waits with no time limit.
- A break lasts the break length, and nothing is blocked during it. The user can skip the break.
- [ASSUMPTION: when a break ends, the end-of-session sound plays if it is on, and the user starts the next session from the extension; nothing starts automatically.]

#### FR-7: Pause and resume when Chrome closes
If Chrome is closed, crashes or the PC sleeps while a session is running, the session pauses with its remaining time. When Chrome opens again, it resumes automatically.
- Blocking is active again as soon as the session resumes.
- There is no time limit on the pause.
- A resumed session that is completed counts for the day it ends (FR-17).

### 4.2 Blocking and Warning

**Description:** During a running session, opening a blocklisted site shows a warning window over the page. The user has 10 seconds to leave the site. Staying, or pressing "Abort session", aborts the session. After a completed session, blocklisted sites show a reminder window until the end-of-session choice is made. Realizes UJ-1, UJ-2.

#### FR-8: Edit the blocklist
The user can add and remove sites on the blocklist. The default blocklist contains YouTube, TikTok, Instagram and Reddit. Realizes UJ-4.
- Changes apply to the next site opened, including during a running session.

#### FR-9: Show the warning window
When the user opens a blocklisted site during a running session, the warning window appears over the page. Realizes UJ-1, UJ-2.
- The window appears within 1 second of the site opening, with the page visible behind it.
- It shows a 10-second countdown blinking red and a text telling the user to leave the site to keep the session.
- It has an "Abort session" button and no other way to close it.
- Only blocklisted sites trigger it. Switching to another program, such as VS Code, does not.

#### FR-10: Keep the session by leaving
If the user leaves the blocklisted site within 10 seconds, the session continues uninterrupted. Realizes UJ-1.
- "Leaving" means the tab no longer shows a blocklisted site, either because it was closed or because it moved to another site.

#### FR-11: Abort the session
If the countdown reaches zero while the user is still on the site, or the user presses "Abort session", the session is aborted and adds no focus minutes. Realizes UJ-2.
- "Abort session" aborts immediately, with no confirmation step.
- After an abort, the window stays on screen and asks, in a neutral tone, whether the user wants to start a new session.
- Declining closes the window and leaves the site open as normal.
- Accepting while on a blocklisted site starts a new session and shows a new warning window with a new 10-second countdown.

#### FR-12: Show the reminder window
After a session is completed and before the end-of-session choice is made, opening a blocklisted site shows the reminder window (D-3). Realizes UJ-1.
- It says the session is finished, has no countdown and cannot cause any loss.
- It offers the end-of-session choice. A break leaves the site open; a new session shows the warning window as in FR-9.
- It appears again on blocklisted sites until the choice is made.

#### FR-13: No blocking outside sessions
Outside a running session, and outside the reminder period in FR-12, blocklisted sites open normally.

### 4.3 The City

**Description:** The user builds a city one building at a time. Each completed session adds focus minutes to the building under construction. When it is finished, it stands in the city and the next one starts. Realizes UJ-3, UJ-4.

#### FR-14: Show the city
The user can see the city: all finished buildings and the building under construction, with a progress bar showing its focus minutes against what it needs. Realizes UJ-3, UJ-4.
- On first use, the city is empty and shows a Type 1 building under construction with an empty progress bar.

#### FR-15: Finish a building
When the building under construction reaches its required focus minutes, it is finished and appears in the city. Realizes UJ-3.
- Focus minutes left over go to the next building under construction.
- The same building type can be built any number of times.

#### FR-16: Pick the next building
The user can pick the next building type from a menu of Type 1 to Type 5. Realizes UJ-3.
- If the user does not pick, the same type as the last building is used. Before the first building, Type 1 is used.
- The pick can be changed until the next session starts. It is then locked until that building is finished.

### 4.4 Streak

**Description:** The streak counts consecutive days with at least one completed session. It is shown as a number and does not affect the city.

#### FR-17: Count the streak
A calendar day in local time with at least one completed session extends the streak by one. A day without one resets it to zero.
- A session that crosses midnight counts for the day it ends.
- Aborted sessions do not count.
- Demo-mode sessions never count toward the streak.

#### FR-18: Show the streak
The streak is shown as a number next to the city.

### 4.5 Demo Mode

**Description:** Demo mode lets the group show a full session and a finished building at the presentation without waiting hours. It runs on a separate demo city.

#### FR-19: Turn demo mode on and off
The user can turn demo mode on and off from a setting that is out of the way, so normal users do not switch it on by accident.

#### FR-20: Faster time in demo mode
In demo mode, 1 real second counts as 1 minute for session lengths, break lengths and focus minutes.
- A 25-minute session takes 25 seconds, and a Type 1 building takes about 1 minute of real time.
- The 10-second countdown in the warning window still runs in real time.

#### FR-21: Separate demo data
Demo mode uses the demo city. Turning demo mode off brings back the real city and streak exactly as they were.
- Demo focus minutes are never added to the real city.

## 5. Cross-Cutting Requirements

- **NFR-1 Privacy:** Sites are checked against the blocklist only while a session is running or the reminder window is in effect. Browsing history is never stored or sent anywhere.
- **NFR-2 Local storage:** Sessions, the city, the streak, the blocklist and settings are stored locally in the browser. There is no login and no server.
- **NFR-3 Persistence:** Progress survives closing and reopening the browser.
- **NFR-4 Responsiveness:** The extension opens and is usable within 1 second. The warning window appears within 1 second (FR-9).
- **NFR-5 Light by design:** Focus minutes are the only progress unit. There are no coins, gems or other currencies.
- **NFR-6 Testing:** Blocking (FR-8 to FR-13) is verified with a documented manual test plan. Session, city, streak and demo rules (FR-4, FR-6, FR-7, FR-14 to FR-21) are covered by unit tests.
- **NFR-7 Platform:** Chrome on desktop, as a Manifest V3 extension.

## 6. MVP Scope

### 6.1 In Scope
- Features 4.1 to 4.5 and the requirements in §5.
- Stretch goal from the brief: building types unlocked through a skill tree. It ships in v1 if there is time, otherwise as a fast follow.

### 6.2 Out of Scope for v1
- Browsers other than Chrome.
- The phone app, and syncing progress between devices.
- Accounts, cloud backup and sharing cities.
- Names and art for the building types (decided with UX).
- More than one city theme.

## 7. Success Metrics

v1 is a graded course project. It succeeds when each requirement can be demonstrated, using demo mode where real time would be too long.

- **SM-1:** Every scenario in the manual test plan for blocking passes. Validates FR-8 to FR-13.
- **SM-2:** All unit tests for session, city, streak and demo rules pass. Validates FR-4, FR-6, FR-7, FR-14 to FR-21.
- **SM-3:** In a live demo, a session is started in two clicks and a building is finished. Validates FR-1, FR-15, FR-20.

**Counter-metric**
- **SM-C1:** The number of warnings shown should not be pushed up. More warnings means more drifting, not a better product. Counterbalances SM-1.

## 8. Open Questions

1. **Warning sound.** Whether the warning window plays a sound is still open. It is to be tested in the technical spike.
2. **Blocking feasibility.** The spike has not been built, so showing the warning window over a page within 1 second in Manifest V3 is still unproven (D-4).
3. **Ending a session early.** Apart from "Abort session" in the warning window, there is no way to end a running session. Should the extension itself offer one, and does it count as an abort?
4. **Building names and look.** Type 1 to Type 5 are placeholders.

## 9. Assumptions Index

- FR-2: session and break lengths are whole minutes between 1 and 120.
- FR-6: when a break ends, the sound plays if it is on, and the next session is started by the user.
