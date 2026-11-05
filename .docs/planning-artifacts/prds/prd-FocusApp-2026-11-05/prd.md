---
title: Focus App
status: draft
created: 2026-11-05
updated: 2026-11-05
---

# PRD: Focus App

## 2. Target User

Anyone doing concentrated work at a PC, whether for a job, for school or to learn something in their spare time, who drifts to distracting sites by reflex. This is wider than the brief, which names students and self-directed learners.

### 2.1 Key User Journeys

**UJ-1. Ida finishes a focus session and sees her city grow.**
- **Persona + context:** Ida is teaching herself programming in her spare time. It takes concentration, and she knows she drifts to distracting sites without deciding to.
- **Entry state:** At her PC, working in Chrome or in another program such as VS Code. The extension is installed. No login is needed. [ASSUMPTION: no setup is needed before the first session.]
- **Path:**
  1. Ida starts a session from the extension, with the length she has chosen.
  2. A timer counts down while she works, shown the way she has chosen: full screen on a screen of its own, a small window in the corner of the browser, or not at all.
  3. By reflex, she opens a blocklisted site. A warning window appears over the page, with a 10-second countdown blinking red and a text telling her to leave the site to keep the session.
  4. She leaves the site within the 10 seconds, and the session continues.
- **Climax:** The timer reaches zero. A visual cue tells her she has done something good, a sound plays if she has turned it on, and she sees how much the progress bar of the building under construction has grown.
- **Resolution:** She chooses between starting a new session and starting a break, during which she can visit any site. The choice waits until she makes it.
- **Edge case:** With the timer hidden and the sound off, nothing interrupts Ida when the session ends. This is deliberate: she is probably deep in her work, and a notice could break her focus. The minutes are added anyway, and she sees the result the next time she opens the extension.

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
- **Resolution:** She picks the next building from a menu of the five building types, which need 1, 2, 3, 4 and 5 hours of focus minutes. If she does not pick one, the same type as last time is built.
- **Edge cases:**
  - [ASSUMPTION: she can pick until the next session starts. The building is then locked, as the brief does not allow switching mid-construction.]
  - [ASSUMPTION: minutes left over when a building is finished go to the next building.]
  - [ASSUMPTION: before her first building there is no "last time", so the 1-hour type is preselected and she can start a session without choosing.]
