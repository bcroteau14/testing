# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This directory contains a single self-contained HTML file: [tictactoe.html](tictactoe.html). There is no build system, package manager, or external dependencies — open the file directly in a browser to run it.

## Architecture

Everything lives in one file with three co-located sections:

- **CSS** (`<style>`) — dark/light theme via `.light` class toggled on `<body>`, cell states via `.taken`, `.x`, `.o`, `.win` classes
- **HTML** — static 3×3 grid of `.cell` divs with `data-i` indices 0–8; score display; status line; reset and theme-toggle buttons
- **JS** (`<script>`) — no framework; `board[]` array tracks state, `WINS` defines all 8 winning combos, `checkWin()` scans them after each move; scores persist in a `scores` object for the session (reset on page reload)
