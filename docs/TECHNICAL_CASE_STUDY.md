# Technical Case Study: 2D Mario

An engineering write-up of a small Python/pygame platformer. It is based on read-only inspection of the project plus the changes made in a working copy. No source is reproduced.

## 1. Product context

A single-player, pirate-themed platformer for desktop: world map, three levels, coins, patrolling enemies, a goal flag. It is a compact exercise in building a complete game loop with a small dependency footprint (Python and pygame only).

## 2. What is real and what is simple

| Area | Reality |
|---|---|
| Gameplay | Real, playable: movement, jumping, gravity, stomping, damage, goal, unlocks |
| Enemy behaviour | Rule-based patrol with reverse-at-constraint; no AI or machine learning |
| Levels | Three authored in Tiled; map nodes 4 to 6 are locked placeholders with no level data |
| Persistence | None; progress lasts for the session |
| Multiplayer / online | None |
| Visual effects | Procedural, drawn in code |

## 3. Design

- A game object holds run state and a state machine; the map and levels are separate objects connected by callbacks.
- Levels are data: Tiled CSV layers plus a table of paths and metadata. Adding a level means adding layers and a table entry.
- The player is a small animation state machine (idle, run, jump, fall) with axis-by-axis collision against terrain, crates and foreground palms.

## 4. Polish pass

| Feature | Approach |
|---|---|
| Title screen | Wavy outlined logo text on a drawn wooden plank, blinking prompt, live level backdrop with a frozen player |
| HUD | Ten hearts at 10 hp each plus a smooth bar; coin icon with a bump on pickup; level banner; timer; score |
| Parallax | Sky gradient, sun, distant hills and sea, boats and clouds scrolling at different rates |
| Particles | Coin sparkles and "+N" popups, jump, land and run dust, enemy burst, sea splash, goal confetti |
| Feedback | Screen shake and a red vignette on damage |
| Camera | Eased follow with look-ahead in the facing direction, clamped to the level |
| Pause | Overlay on a snapshot of the last frame; audio paused; resume, restart, quit |
| Results | Slide-in card, count-up rows, stars, confetti; separate game-over screen |
| Map | Name tags, padlocks, completion ticks, best score, animated route, selection halo |

## 5. Scoring

Coins x10, stomps x100, and a time bonus of (90 minus seconds, floored at 0) x5. One to three stars depending on the share of coin value collected. Best result per level is kept for the session.

## 6. How the screenshots were produced

A capture script runs the real game in-process with a dummy video and audio driver and a virtual 60 fps clock, sends scripted key events and saves the actual render surface. Level movement comes from a small look-ahead bot that jumps walls, gaps and enemies. Pause, quit, level-complete and game-over states are reached through the normal game flow. The game-over frame uses the real damage path after setting health low.

## 7. Limits

Desktop only, no web build. Assets load with relative paths, so the game must be started from its code directory. Three playable levels; no saves; no settings menu.
