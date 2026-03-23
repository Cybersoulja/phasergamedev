# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Phaser 3 game project using a single-file architecture. No build step or package manager is needed — Phaser 3.20.0 is loaded from CDN and the game runs directly in the browser.

## Running the Game

Clone the repo and serve with any static file server — no build step needed:

```bash
git clone <repo-url>
cd phasergamedev
python3 -m http.server 8080
# then open http://localhost:8080
```

On Replit, `static-web-server` is used automatically on port 80.

## Architecture

- **`index.html`** — The entire game. Contains the Phaser config and three lifecycle callbacks:
  - `preload()` — Load assets from the `/assets/` directory
  - `create()` — Set up sprites, physics, input handlers
  - `update()` — Per-frame game loop logic
- **`assets/`** — Sprites: `sky.png`, `platform.png`, `dude.png`, `star.png`, `bomb.png`

## Phaser 3 Patterns

- Game canvas: 800×600, renderer: `Phaser.AUTO`
- Load assets in `preload()` using `this.load.image(key, path)` or `this.load.spritesheet()`
- Create objects in `create()` using `this.add.*`, `this.physics.*`, `this.input.*`
- The scene context (`this`) is the Phaser.Scene instance in all three callbacks

## Development Notes

- No tests, no linter, no TypeScript compilation — edit `index.html` directly
- Replit auto-deploys as a static site; the entrypoint is `index.html`
