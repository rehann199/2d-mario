# Product Overview

All screenshots on this page are real captures of a local build of the game, taken from the render surface by a scripted run. The game is single-player and runs locally on a desktop; there is no online component.

## What it is

2D Mario is a pirate-themed, Mario-style side-scrolling platformer written in Python with pygame. The player picks a level from a world map, runs and jumps across islands, collects coins, stomps patrolling enemies and reaches the goal flag. Three levels are playable; three further map nodes are locked placeholders.

The project grew out of a staged tutorial-style codebase. This showcase covers the final stage, extended with a presentation pass: title screen, HUD, parallax backdrop, particle effects, pause menu and result screens.

## Flow

<table>
  <tr>
    <td width="50%"><img src="../assets/screenshots/2d-mario-title.webp" alt="Title screen with wooden logo plank and a blinking Press Enter prompt over a live level backdrop"></td>
    <td width="50%"><img src="../assets/screenshots/2d-mario-overworld.webp" alt="World map with the first level open and the other nodes locked"></td>
  </tr>
  <tr>
    <td>Title screen. The backdrop is an inert copy of level 1 with patrolling enemies.</td>
    <td>World map. Open nodes are animated; locked nodes are dimmed with a padlock and "???".</td>
  </tr>
</table>

## In a level

<table>
  <tr>
    <td width="50%"><img src="../assets/screenshots/2d-mario-level1-shipwreck-shore.webp" alt="Shipwreck Shore level mid-jump with HUD, stomp particles and a plus-100 popup"></td>
    <td width="50%"><img src="../assets/screenshots/2d-mario-level2-crate-cliffs.webp" alt="Crate Cliffs level with floating platforms, crates and an enemy"></td>
  </tr>
  <tr>
    <td>Shipwreck Shore. Hearts and health bar, coin counter, level name, time and score.</td>
    <td>Crate Cliffs. Floating platforms and crates over parallax sea and hills.</td>
  </tr>
  <tr>
    <td><img src="../assets/screenshots/2d-mario-level3-palm-reef.webp" alt="Palm Reef level with an enemy-defeat particle burst"></td>
    <td><img src="../assets/screenshots/2d-mario-hud-coins-sparkles.webp" alt="Coin pickup with sparkles, plus-1 popup and the coin counter highlighted"></td>
  </tr>
  <tr>
    <td>Palm Reef. Stomping an enemy triggers a burst and +100.</td>
    <td>Coin pickup: sparkles, a "+N" popup and a counter bump.</td>
  </tr>
</table>

## Menus and results

<table>
  <tr>
    <td width="50%"><img src="../assets/screenshots/2d-mario-pause-menu.webp" alt="Pause menu with Resume, Restart level and Quit to map"></td>
    <td width="50%"><img src="../assets/screenshots/2d-mario-level-complete.webp" alt="Level complete card with coin, stomp and time rows, score and one star"></td>
  </tr>
  <tr>
    <td>Pause (ESC or P): resume, restart the level or quit to the map.</td>
    <td>Level complete: coins, stomps, time, score and 1 to 3 stars.</td>
  </tr>
  <tr>
    <td><img src="../assets/screenshots/2d-mario-overworld-progress.webp" alt="World map after completing level 2, showing a completion tick, best score and the next level selected"></td>
    <td><img src="../assets/screenshots/2d-mario-game-over.webp" alt="Game over screen with skull and crossbones, coins and score"></td>
  </tr>
  <tr>
    <td>Map after a win: completion tick, best score, route to the next level.</td>
    <td>Game over when health reaches zero; Enter starts a fresh run.</td>
  </tr>
</table>

## Controls

| Where | Keys |
|---|---|
| Title | Enter to start |
| Map | Left / Right travel, Space or Enter to enter a level, Esc to return to title |
| Level | Left / Right run, Space jump, Esc or P pause |
| Menus and result screens | Up / Down, Enter |

## Rules in brief

- 100 health, 10 damage per enemy touch, short invincibility blink afterwards.
- Jumping on an enemy defeats it; touching it from the side hurts.
- Falling into the sea sends the player back to the map and drops that attempt's coins.
- Score is coins x10, plus stomps x100, plus a time bonus that shrinks over 90 seconds. Stars come from the share of coin value collected.
- No saves: progress lasts for the session.

A short looping gameplay clip is in [`assets/`](../assets/) as `2d-mario-gameplay.mp4` and `.gif`.
