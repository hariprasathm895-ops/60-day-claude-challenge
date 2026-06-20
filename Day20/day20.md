# Day 20 — Face Puzzle Game

## Overview
Built a complete, self-contained face puzzle game as a single HTML file.
Users take a photo of themselves with their webcam (or upload one), the
photo is sliced into a grid, scrambled, and the player drags pieces back
into place against a live timer and move counter.

**File:** `face-puzzle-game.html` — no frameworks, no build step, all CSS
and JS inline. Loads with zero external dependencies.

## Features Built

### Camera capture
- `getUserMedia()` requests front-facing camera access on load
- Live mirrored video preview inside a viewfinder-style frame
- "Take Photo" shutter button snapshots the feed onto a canvas
- Graceful fallback: permission-denied / no-camera messaging, plus an
  "upload a photo instead" option using a file input

### Puzzle generation
- Difficulty choice: 3×3, 4×4, or 5×5
- Captured photo sliced into equal canvas pieces per grid size
- Pieces shuffled with Fisher–Yates (re-shuffled if it lands on the solved
  state) — every shuffle is solvable since any two tiles can be swapped
  directly, with no blank-tile restriction

### Drag & touch controls
- Built on the Pointer Events API so mouse drag and touch drag share one
  code path instead of two separate handlers
- Dragged tile gets an amber highlight border
- Correctly placed tiles get a green border, live, as you play
- Drop target gets a white hover highlight; pieces swap and snap into
  place on release

### Timer & move counter
- Timer starts the moment the puzzle begins, formatted mm:ss.t
- Move counter increments only on a real swap (not on a no-op drop)
- Live "placed / total" counter shows correct pieces out of the grid total

### Win detection & results
- Auto-detects when every tile is in its correct position
- Stops the timer immediately and shows a results overlay: final time,
  total moves, grid size
- Saves the top 5 best times to `localStorage` (date, time, moves,
  difficulty), sorted fastest-first
- Leaderboard is viewable from a standalone button at any time, not just
  after winning

### UI & polish
- Dark, camera/darkroom-inspired visual identity (viewfinder corner
  brackets, monospace HUD-style stat readouts, shutter-button capture
  control) instead of a generic template look
- Retake Photo / Play Again / New Photo flows all wired to reset the right
  amount of state (camera stream, board, timer)
- Responsive layout for desktop and mobile, visible focus states, and
  `prefers-reduced-motion` respected

## How It Works (technical notes)
- Captured photo is normalized to a 600×600 square canvas (divisible
  cleanly by 3, 4, and 5) before slicing
- Each puzzle piece is its own cropped canvas converted to a JPEG data URL
  and used as a tile's background image
- `board[]` maps each grid cell to the piece currently sitting in it;
  a cell is "correct" when `board[cell] === cell`
- Swaps happen by dragging any tile onto any other occupied cell —
  `document.elementFromPoint()` is used during drag to detect the tile
  under the pointer

## Learnings
- Pointer Events meaningfully simplify drag-and-drop — one set of handlers
  covers both mouse and touch instead of maintaining two.
- A free-swap puzzle (any tile can swap with any other) sidesteps the
  classic "is this shuffle solvable" problem that sliding-tile puzzles
  have to solve for.
- Camera permission handling needs a real fallback path, not just an
  error message — adding a file-upload option kept the game playable
  even without webcam access.
- Small visual choices (viewfinder brackets, monospace stat readouts)
  go a long way toward making a generated app feel designed rather than
  templated.

## Screenshots
_Add screenshots here: camera permission prompt, photo capture, difficulty
selection, mid-game drag interaction, win screen, and leaderboard._

## Technologies
HTML5 · CSS3 · JavaScript · `getUserMedia()` · Pointer Events API ·
Canvas API · localStorage · Claude AI
