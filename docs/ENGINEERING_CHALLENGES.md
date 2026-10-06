# Engineering Challenges

Five problems from the project. Outcomes describe observable behaviour; no performance metrics are claimed.

---

## 1. Keeping a scrolling world and a moving player consistent

**Problem**
The level scrolls by shifting every sprite, while the player collides in screen space. A camera that moves the world in the same frame as collision resolution makes the player drift or jitter.

**Approach**
- The camera computes an integer shift and applies it to the next frame; the player's collision box is compensated by last frame's shift before movement.
- Follow is eased toward the player with a look-ahead in the facing direction, speed-capped, and clamped to the level width.

**Outcome**
Smooth follow without moving the player relative to the terrain.

---

## 2. A HUD that stays still under screen shake

**Problem**
Damage and stomps shake the screen, but a shaking HUD is hard to read.

**Approach**
- Shake is applied to the world render only, then the hit flash; the game object draws the HUD afterwards.
- Shake uses a decaying "trauma" value so strong hits shake harder and settle quickly.

---

## 3. Particles that follow the world

**Problem**
Dust, sparkles and bursts are spawned in world space while the camera moves.

**Approach**
- Each particle is shifted by the same per-frame scroll as the sprites.
- One small particle system supports circles, squares, stars, rings and text popups, so every effect shares the update and draw path.

---

## 4. A crash when a level ends itself

**Problem**
Falling into the sea ended the level inside its own update and cleared the level reference. The HUD, drawn right after, then used a level that no longer existed.

**Approach**
- Found by running a scripted bot through the levels. The main loop now returns early when the level has ended or the state has changed.

**Outcome**
Sea falls return to the map cleanly, and the capture run covers the path.

---

## 5. Testing a game without a display

**Problem**
Producing reliable frames from a windowed game on a machine that cannot screen-capture.

**Approach**
- Headless SDL drivers, a virtual clock for deterministic timing, and in-process saves of the render surface.
- A small ballistic look-ahead decides jumps; the script retries if the bot falls.

**Limitation**
The bot is simple and does not clear every level, so frames come from the stretches it does play.
