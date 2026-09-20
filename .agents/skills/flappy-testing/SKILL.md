---
name: play-test-flappy-bird
description: Play-test the standalone canvas game with real inputs, collision checks, and persistent high-score verification.
---

# Local environment
- Open `index.html` directly in Chrome using its absolute `file://` URL; no server, build, or dependency installation is required.
- Start in a fresh browser profile when previous testing may have changed storage or installed browser instrumentation. Keep the same profile and URL for persistence checks.
- Maximize the browser before recording. On Linux, use `wmctrl -r :ACTIVE: -b add,maximized_vert,maximized_horz`.

# Devin Secrets Needed
None.

# Runtime testing
- Verify start text and high score, Space/click/touch-emulated start and flap, then ground, top, and pipe collisions independently.
- The canvas is 400×600. A pipe first appears around 0.75 seconds after starting; score is earned only after the pipe's trailing edge passes the bird, roughly 3.1 seconds after start.
- For timing-sensitive automation, inspect rendered canvas pixels and dispatch real keyboard/mouse/CDP touch events. Do not change game state, physics, random generation, or scores.
- Screenshot capture consumes real gameplay time. Avoid blocking input control on screenshots when approaching collisions.
- Stop repeated input as soon as Game Over appears; another input immediately restarts. Yellow high-score text can be mistaken for the yellow bird in naive pixel detection; independently detect the red Game Over heading.
- Earn a nonzero score naturally, end the game, restart for a lower score, then reload. Verify both visible high score and read-only `localStorage.getItem("flappyHighScore")`.
- Chrome touch emulation covers the touch handler, not physical mobile-device behavior.
