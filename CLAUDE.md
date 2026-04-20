# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A personal testing sandbox — self-contained browser games and experiments. No build system, package manager, or external dependencies. Every file opens directly in a browser.

## Git Workflow

After every meaningful change, commit and push to [bcroteau14/testing](https://github.com/bcroteau14/testing) so work is never lost:

```bash
git add <changed files>
git commit -m "short description of what changed and why"
git push
```

Commit messages should be concise and specific — describe the change, not the process (e.g. `"add ball speed cap to Pong"` not `"made some updates"`). Commit at logical stopping points: after adding a feature, fixing a bug, or any edit the user approves.

## Running the Games

Open any HTML file directly in a browser — no server required:
- [tictactoe.html](tictactoe.html) — two-player Tic Tac Toe
- [pong.html](pong.html) — single-player Pong vs AI

## Shared Architecture Patterns

Both games follow the same conventions; new files should too:

- **Single HTML file** — `<style>`, HTML, and `<script>` co-located in one file, no external JS/CSS beyond Google Fonts
- **Dark/light theme** — default dark; `.light` class toggled on `<body>` via a fixed top-right button; all color overrides live under `body.light { }` selectors
- **Session scoring** — a plain JS object (e.g. `scores`, `matchWins`) tracks wins for the session; resets on page reload, never persisted to `localStorage`
- **No frameworks** — vanilla JS only; DOM queried with `querySelector`/`querySelectorAll`

## Game-Specific Notes

### tictactoe.html
- `board[]` (length 9) holds `null | 'X' | 'O'`; `WINS` lists all 8 winning index triples
- `checkWin()` scans `WINS` after every move; draw detected via `board.every(Boolean)`

### pong.html
- Rendering via `<canvas>` (600×400) with `requestAnimationFrame`; all drawing happens in `draw()`, all physics in `update()`
- State machine: `STATE.WAITING → PLAYING → POINT → PLAYING` (loops) or `→ WON`
- Theme colors are read into a `theme` object each frame via `updateTheme()` — canvas redraws automatically reflect light/dark switches
- AI paddle tracks ball Y with a speed cap (`AI_SPEED = 3.8`) and intentional error offset (`AI_ERROR = 18px`) to keep it beatable
- Ball speed increases by 0.3 per volley, capped at `BALL_MAX_SPEED = 10`; angle varies based on where the ball hits the paddle
