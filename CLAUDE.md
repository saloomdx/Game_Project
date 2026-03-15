# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A collection of browser-based arcade games. No build tools, frameworks, or package managers — every game is a single self-contained HTML file with vanilla JS and Canvas.

## Running Games

Open any HTML file directly in a browser — no server needed:

```
start claude/tictactoe.html
start claude/shooter.html
```

## Repository Structure

```
Game_Project/
├── claude/
│   ├── tictactoe.html   # Tic-Tac-Toe game
│   └── shooter.html     # Top-down retro arcade shooter
└── .gitignore
```

All new games go inside the `claude/` folder.

## Architecture Pattern

Each game is a **single HTML file** following this structure:

1. `<style>` — layout and UI styling (dark theme, centered canvas)
2. `<canvas>` — the game renders entirely onto a canvas element
3. `<script>` — all game logic in one script block:
   - Constants / state variables at the top
   - `init()` — resets game state
   - `update()` — game logic, called every frame
   - `draw*()` — rendering functions
   - `loop()` — ties update + render together via `requestAnimationFrame`

## Game-Specific Notes

### shooter.html
- Game states: `MENU → PLAYING → LEVEL_CLEAR → GAME_OVER`
- Canvas is 800×600, scaled responsively via CSS
- Enemy types unlock by level: Basic (lv1), Fast (lv2), Shooter (lv3), Tank (lv5)
- High score persisted in `localStorage` under key `retroShooterHS`
- Speeds to keep gameplay comfortable: player `2.0`, basic `0.6`, fast `1.1`, shooter `0.45`, tank `0.3`

### tictactoe.html
- CPU uses full minimax (unbeatable at optimal play)
- Score tracking lives in the `scores` object `{ X, O, tie }`; persists across rounds but resets on "New Game"
- After a win/tie, board auto-resets after 2200 ms

## Git Workflow

The repo is on GitHub at `https://github.com/saloomdx/Game_Project`.

**Commit and push after every meaningful unit of work** — completing a feature, fixing a bug, creating a new file, or making any change worth keeping. Never leave work uncommitted at the end of a session. This ensures we can always revert to a safe state.

```bash
git add <files>
git commit -m "descriptive message"
git push
```

Commit message format:
- Use the imperative mood: `Add`, `Fix`, `Update`, `Remove`
- Be specific: `Fix shooter enemy spawn rate on level 3` not `Fix bug`
- Keep the subject line under 72 characters
