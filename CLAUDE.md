# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Browser-based game portfolio. Each game is a **single self-contained HTML file** with embedded CSS and vanilla JavaScript — no build system, no dependencies, no external assets.

## Running Games

Open any `.html` file directly in a browser. No server required.

On Windows: `cmd.exe /c start "" "path\to\file.html"`

## Architecture

All games follow the same single-file pattern:
- **HTML structure** with a `<style>` block and one `<script>` block
- **No external dependencies** — all sprites/graphics drawn programmatically (Canvas API or DOM)
- **Dark retro theme** — consistent color palette (`#0a0a1a` background, `#e94560` accent)

### VOID SURVIVORS (`shooter.html`) — Canvas-based arcade shooter

Code is organized into labeled sections in this order:
1. **Constants & Config** — `COLORS` object, `LEVELS` array (10 wave definitions)
2. **Input** — polled keyboard/mouse state object
3. **Game State** — `game` and `player` plain objects (no classes)
4. **Utilities** — collision detection, edge spawning, particle factory
5. **Sprite Drawing** — one `draw*()` function per entity type, all using canvas primitives
6. **Enemy Creation** — factory function returning enemy objects by type string
7. **Level Management** — `startLevel()` builds a shuffled spawn queue
8. **Update** — state machine (`MENU`/`PLAYING`/`LEVEL_CLEAR`/`GAME_OVER`), runs at fixed 60 FPS timestep
9. **Render** — draws grid, entities, HUD, overlay screens
10. **Game Loop** — `requestAnimationFrame` with accumulator pattern

Key patterns: state machine for game flow, circle-circle collision, particle arrays with lifetime decay, screen shake via canvas translate offset, localStorage for hi-score persistence.

### Tic Tac Toe (`tictactoe.html`) — DOM-based

Simple click-handler game using HTML buttons. Win detection via predefined line arrays.

## Git Workflow

Commit and push to GitHub regularly as you work — after each meaningful change or completed feature. Never leave work uncommitted. Use clean, descriptive commit messages that explain *why* the change was made. Push to `origin main` after every commit so that work is always backed up on GitHub and easy to revert if needed.

## Conventions

- Games must work by opening the HTML file directly (no server, no bundler)
- All visuals drawn with code — no image files or sprite sheets
- `imageSmoothingEnabled = false` for crisp pixel-art edges on canvas games
- Keep entity data as plain objects, not classes
- Git remote: https://github.com/nkimmes11/ClaudeCodeTest
