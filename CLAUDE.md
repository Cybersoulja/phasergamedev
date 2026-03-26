# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A Phaser 3 game project using a single-file architecture. Phaser 3.20.0 is loaded from CDN and the game runs directly in the browser. No build step is required for the game itself — dev tooling (Vite, ESLint, Prettier) is managed via npm.

## Running the Game

```bash
npm install
npm run dev        # Vite dev server on http://localhost:5173 with HMR
```

Or serve statically without npm:

```bash
python3 -m http.server 8080
```

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

## Dev Tooling

| Command | What it does |
|---|---|
| `npm run dev` | Vite dev server with HMR |
| `npm run lint` | htmlhint + eslint on `index.html` |
| `npm run lint:fix` | Auto-fix ESLint issues |
| `npm run format` | Prettier write |
| `npm run format:check` | Prettier check (no write) |

- **ESLint** — lints inline `<script>` blocks via `eslint-plugin-html`; `Phaser` is declared as a global in `.eslintrc.json`
- **Prettier** — formats HTML/JS; config in `.prettierrc`
- **Vite** — dev server only; no bundling/build output

## Deployment

Deployed to Cloudflare via `wrangler.jsonc`. The root directory is served as static assets. Dev-only files are excluded via `.wranglerignore`.
