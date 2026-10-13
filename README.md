# 2048
A 2048 clone. A from-scratch implementation of the 2048 sliding-tile puzzle. One HTML file, vanilla JavaScript, no dependencies or build step.

## Run it

Open `2048.html` in any modern browser. That's it.

## How to play

Slide all tiles in one direction. Tiles with the same number merge into one tile with their sum. After every move that changes the board, a new 2 (90%) or 4 (10%) appears. Reach the 2048 tile to win. The game ends when the board is full and no merges are possible.

## Controls

| Input | Action |
| --- | --- |
| Arrow keys or WASD | Move tiles |
| Swipe on the board | Move tiles (touchscreens) |
| New game button | Restart |

## Features

- 4×4 board with animated slide, spawn, and merge effects
- Score and best score; best score persists via `localStorage`
- Win screen at 2048 with an option to keep playing
- Game-over detection
- Light and dark themes (follows the system setting)
- Responsive layout; respects `prefers-reduced-motion`

## How it works

- **Board state:** a 4×4 array of tile objects (`{id, v}`) or `null`. Each tile has a stable `id`, so the DOM element is reused and CSS transitions animate it between cells.
- **Moves:** every direction is treated as sliding a single line toward index 0. `move(dir)` extracts each row or column in the right order, passes it to `slide()`, and writes the result back.
- **`slide(line)`:** drops empty cells, merges equal neighbours once per move (so `[2,2,2,2]` becomes `[4,4]`, not `[8]`), and pads with `null`. It reports whether anything changed, and the score gained.
- **No-op moves:** if nothing moved, no tile spawns, so invalid moves don't advance the game.
- **Game over:** the board is full and no adjacent tiles (horizontal or vertical) share a value.

## Project structure

```
2048.html   markup, styles, and game logic in one file
README.md   this file
```

## Ideas for extending it

- Undo last move
- Configurable board size (3×3, 5×5, 6×6)
- Move animations for merges that slide both tiles before combining
- Keyboard-free "hint" using a simple expectimax search
- Saved game state across reloads

## License

MIT. Use it however you like.
