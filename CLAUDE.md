# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Snail Betting is a web-based snail racing/betting game inspired by Camel Up. Players watch 6 colored snails race across a 12-space track and place bets on the winner. Earlier bets pay better odds (5x/3x/2x/1.5x based on leading snail position).

## Architecture

Single-file application: everything lives in `index.html` — HTML structure, CSS styles, and vanilla JS game engine are all inline. Zero dependencies, no build step, no framework.

**To run:** Open `index.html` in a browser. No server required.

**Three screens** managed by toggling `.active` class: setup (player count/names), game (track + betting + dice), game over (standings + high score).

**Game state** is a single `state` object holding players, snails (position array), current turn, round counter, and bets. All game logic functions (`rollDice`, `moveSnails`, `placeBet`, `resolveBets`, `checkWin`) read/mutate this object.

**Rendering** uses safe DOM manipulation (`textContent`, `createElement`) — no `innerHTML` with user-controlled data. Player names are escaped via `escapeHTML()`.

## Key Constraints

- Must work on iOS Safari (mobile-first, touch targets >= 44px, `100dvh` viewport)
- All user input (player names) must be sanitized — never use `innerHTML` with untrusted content
- High score persistence uses `localStorage` (key: `snailBettingHighScore`, single-player only)
