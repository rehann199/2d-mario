<div align="center">

# 2D Mario

**A pirate-themed, Mario-style 2D platformer for desktop: world map, three levels, coins, stomping, particles and a full set of menus.**

Python · pygame · Tiled (CSV level layers) · single-player, offline

![Python](https://img.shields.io/badge/Python-3-3776AB?logo=python&logoColor=white)
![pygame](https://img.shields.io/badge/pygame-2.6-2C8E3C)
![Tiled](https://img.shields.io/badge/Tiled-level%20editor-1E90FF)
![Desktop](https://img.shields.io/badge/Desktop-local%20app-555555)

<table>
  <tr>
    <td><img src="assets/screenshots/2d-mario-title.webp" width="300" alt="Title screen with a wooden 2D Mario logo plank and a Press Enter prompt over a level backdrop" /></td>
    <td><img src="assets/screenshots/2d-mario-level1-shipwreck-shore.webp" width="300" alt="Shipwreck Shore level mid-jump with hearts, coin counter, timer, score and stomp particles" /></td>
    <td><img src="assets/screenshots/2d-mario-level-complete.webp" width="300" alt="Level complete card with coin, stomp and time rows, score and stars" /></td>
  </tr>
</table>
<sub>Screenshots are real captures of a local build running on fictional demo data.</sub>

<img src="assets/2d-mario-gameplay.gif" width="480" alt="Short looping gameplay clip: running, collecting coins, stomping an enemy and reaching the goal" />

</div>

---

## Product at a Glance

| | |
|---|---|
| **What it is** | A single-player side-scrolling platformer with a world map |
| **Platform** | Desktop (Python and pygame); runs locally, no network |
| **Content** | 3 playable levels; map nodes 4 to 6 are locked placeholders |
| **Gameplay** | Run, jump, collect coins, stomp patrolling enemies, reach the goal flag |
| **Presentation** | Title screen, HUD, parallax backdrop, particles, pause menu, result and game-over screens |
| **Scoring** | Coins, stomps and a time bonus; 1 to 3 stars per level |
| **Levels** | Authored in Tiled, loaded from CSV layers through a data table |
| **Code size** | About 2k lines of Python |

## Product Showcase

<table>
  <tr>
    <td align="center"><img src="assets/screenshots/2d-mario-overworld.webp" width="290" alt="World map with the first level open and others locked"/><br/><sub><b>World map</b><br/>Locks and name tags</sub></td>
    <td align="center"><img src="assets/screenshots/2d-mario-level2-crate-cliffs.webp" width="290" alt="Crate Cliffs level with floating platforms and crates"/><br/><sub><b>Crate Cliffs</b><br/>Floating platforms</sub></td>
    <td align="center"><img src="assets/screenshots/2d-mario-level3-palm-reef.webp" width="290" alt="Palm Reef level with an enemy-defeat burst and plus-100 popup"/><br/><sub><b>Palm Reef</b><br/>Enemy-defeat burst</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="assets/screenshots/2d-mario-hud-coins-sparkles.webp" width="290" alt="Coin pickup with sparkles and the HUD coin counter"/><br/><sub><b>HUD and coins</b><br/>Sparkles, popup, counter</sub></td>
    <td align="center"><img src="assets/screenshots/2d-mario-pause-menu.webp" width="290" alt="Pause menu with Resume, Restart level and Quit to map"/><br/><sub><b>Pause</b><br/>Resume, restart, quit</sub></td>
    <td align="center"><img src="assets/screenshots/2d-mario-overworld-progress.webp" width="290" alt="World map after a win with a completion tick, best score and next level selected"/><br/><sub><b>Progress</b><br/>Ticks and best score</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="assets/screenshots/2d-mario-game-over.webp" width="290" alt="Game over screen with skull and crossbones, coins and score"/><br/><sub><b>Game over</b><br/>Fresh run on Enter</sub></td>
    <td></td>
    <td></td>
  </tr>
</table>

## Key Features

- **Platforming.** Run, jump and fall with an animation state machine; axis-by-axis collision against terrain, crates and foreground palms.
- **Enemies.** Rule-based patrols that reverse at constraint tiles; jump on them to defeat them, touch them from the side to lose 10 health.
- **HUD.** Ten hearts plus a smooth health bar, coin counter with icon, level name, timer and score.
- **Feedback.** Coin sparkles and popups, jump, land and run dust, enemy bursts, sea splash, screen shake and a red hit flash.
- **Camera and backdrop.** Eased follow camera with look-ahead; layered sky, hills, sea, boats and clouds scrolling at different rates.
- **Menus.** Title screen, pause (resume, restart, quit to map), level-complete card with stars and confetti, game-over screen.
- **World map.** Unlockable nodes, name tags, padlocks, completion ticks, best score and an animated route.
- **Audio.** Background music for the map and each level, plus jump, coin, stomp and hit effects.

## Architecture

A `Game` object runs a state machine (title, map, level, paused, complete, game over) and owns the run state. The map and levels are separate objects connected by callbacks. Levels load from Tiled CSV layers into pygame sprite groups through a data table; effects, HUD, screens and decoration live in their own modules.

```mermaid
flowchart LR
    G[Game<br/>state machine] --> O[Overworld]
    G --> L[Level]
    G --> S[Screens + HUD]
    L --> D[Tiled CSV layers<br/>+ level table]
    L --> F[Particles, shake, flash]
    L --> B[Parallax backdrop]
```

Details: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## Engineering Highlights

- **Data-driven levels.** Adding a level means adding Tiled layers and one table entry.
- **Camera and collision.** The world scrolls by shifting sprites; the camera's per-frame shift is compensated so the player does not drift against the terrain.
- **Steady HUD under shake.** Shake and hit flash apply to the world render; the HUD draws afterwards.
- **One particle system.** Circles, squares, stars, rings and text popups share a world-anchored update and draw path.
- **All new UI is code-drawn.** Hearts, padlocks, ticks, stars, panels and the skull use pygame primitives, with no new asset files.
- **Headless capture.** The screenshots come from a scripted in-process run with dummy SDL drivers and a virtual clock.

More: [docs/ENGINEERING_CHALLENGES.md](docs/ENGINEERING_CHALLENGES.md).

## Status & Scope

- **Real:** the playable game, three levels, scoring, menus and effects shown above.
- **Rule-based:** enemy behaviour is scripted patrol. There is no AI or machine learning.
- **Placeholder:** map nodes 4 to 6 are locked and have no level.
- **Not included:** saves (progress lasts for the session), settings menu, online or multiplayer features, a web build.
- Runs locally on a desktop; it must be started from its code directory because assets load by relative path.

## Documentation

- [Product Overview](docs/PRODUCT_OVERVIEW.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Technical Case Study](docs/TECHNICAL_CASE_STUDY.md)
- [Engineering Challenges](docs/ENGINEERING_CHALLENGES.md)
- [Privacy and Source](docs/PRIVACY_AND_SOURCE.md)

## Rights

Source is private and no licence is granted. See [RIGHTS.md](RIGHTS.md).
