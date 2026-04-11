# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A collection of browser-based games built with **vanilla JS, HTML5 Canvas, and CSS** — no build tools, no frameworks, no dependencies. Each game is a single self-contained `.html` file.

## Running the Games

Open any `.html` file directly in a browser. There is no server, build step, or install required:

```
start tictactoe.html
start snake3.html
```

Or via the shell: `cmd.exe /c start "" "<absolute-path>.html"`

## Repository & Git Workflow

- Remote: https://github.com/jacopogrossi-arch/browser-games
- Default branch: `master`
- **Commit and push after every meaningful unit of work** — a new feature, a bug fix, a visual tweak. Never leave work uncommitted at the end of a session.
- Commit messages: imperative mood, describe *what changed and why* (e.g. `Fix self-collision skip distance for 3-headed snake` not `updated snake3.html`).
- Stage specific files by name (`git add snake3.html`) rather than `git add -A` to avoid committing unintended files.
- Always run `git push` immediately after committing so the GitHub remote reflects the latest state and can be used to revert if needed.

## Architecture

Every game follows the same single-file pattern:

```
<head>   — charset, viewport, title
<style>  — all CSS inline (no external sheets)
<body>   — HTML structure (canvas, HUD divs, overlay)
<script> — all game logic (no modules, no imports)
```

### Visual language (shared across all games)

| Token | Value |
|---|---|
| Page background | `#1a1a2e` |
| Surface / arena | `#16213e` |
| Wall / border | `#0f3460` |
| Accent red | `#e94560` |
| Accent cyan | `#a8dadc` |

All new games or UI additions should use these colours to stay visually consistent.

### `snake3.html` — core concepts

- **Trail-based body**: `snake.trail` is a flat `[{x,y}]` array. Index 0 = tail, last = fork point. Growth works by increasing `targetLength` and draining `pendingGrowth` one point per frame.
- **3-head geometry**: `getHeads(snake)` returns three positions fanned out from the fork point using the perpendicular vector `(-sin(angle), cos(angle))`. This is the architectural centrepiece — all collision and rendering branches off it.
- **Game loop**: `requestAnimationFrame` only; no `setInterval`. State machine: `'start' | 'running' | 'dead'`.
- **Persistence**: high score in `localStorage` key `snake3_hi`.

### `tictactoe.html` — core concepts

- Pure DOM (no canvas). Board is a CSS Grid; cells use `data-i` attributes for indexing.
- Win detection iterates `WINS` (8 static triplets) each move.
- Session scores live in a plain object `{ x, o, d }`; no persistence.
