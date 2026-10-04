# AGENTS.md

## Project

Static vanilla-JS Pac-Man (no framework, no build step, no package manager, no dependencies). All code lives in `src/`. Run it by opening `src/index.html` directly in a browser (or serving the folder). There are no tests, linter, typechecker, or npm scripts — verification is manual in the browser (check the console + gameplay).

## Architecture

- Script load order in `src/index.html` is required: `maze.js` → `game.js` → `render.js` → `main.js`. These are plain scripts that share globals via `window` (`MAZE`, `TUNNEL_ROW`, `PACMAN_START`, `GHOST_STARTS`, `createGame`, `update`, `DIRS`, `draw`). Do NOT add ES modules/`import` or reorder the scripts.
- `maze.js` — level data. `MAZE` is the pristine grid; each game copies it so dots can be eaten without destroying the original.
- `game.js` — state and rules: `createGame`, `update`, movement, collision, ghost AI.
- `render.js` — canvas drawing. `TILE=20`, canvas is 560×620.
- `main.js` — requestAnimationFrame loop, keyboard input, start/win/lose overlays.

## Conventions

- Comments, UI strings, and README are in **Spanish**. Keep new text in Spanish.
- Distinctive formatting: 2-space indent and spaces inside parens/brackets: `( x )`, `grid[ y ][ x ]`. Match surrounding code exactly; do not reformat.
- Grid coordinates are cell-based `(x, y)`, origin top-left, 28 cols × 31 rows. Tile codes: `0` empty, `1` wall, `2` dot, `3` pen door. Tunnel row is `TUNNEL_ROW = 14`.

## Spec-driven workflow

- This repo is for learning spec-driven development via the `spec` and `spec-impl` skills in `.agents/skills/` (installed from `klerith/fernando-skills`, pinned in `skills-lock.json`).
- Specs go in `specs/NN-slug.md` (folder does not exist yet; first spec is `01-`). Template: `.agents/skills/spec/template.md`.
- New specs default to `Draft`; a human flips the state to `Approved` before `/spec-impl` will run. `/spec-impl` creates a branch named `spec-NN-slug`, controlled by `specs/.spec-config.yml` `AutoCreateBranch` (default `true`).
- Never auto-implement a spec from this file; the workflow is user-invoked.
