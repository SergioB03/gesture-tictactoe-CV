# Game logic spec

The rules engine for gesture tic-tac-toe. Pure Python, standard library only.
It knows nothing about cameras, hands, or drawing. The vision layer will call it.

## Module

`tictactoe/game.py`

## Public API

```python
class InvalidMove(Exception): ...

class Game:
    def __init__(self) -> None: ...
    @property
    def board(self) -> tuple[tuple[str | None, ...], ...]: ...   # 3x3, None = empty
    @property
    def current_player(self) -> str: ...                         # "X" or "O"
    @property
    def winner(self) -> str | None: ...                          # "X", "O", or None
    @property
    def winning_line(self) -> tuple[tuple[int, int], ...] | None: ...
    @property
    def is_draw(self) -> bool: ...
    @property
    def is_over(self) -> bool: ...
    def place(self, row: int, col: int) -> None: ...
    def reset(self) -> None: ...
```

## Rules

1. The board is 3x3. Rows and columns are numbered 0, 1, 2.
2. "X" always moves first. Players alternate after every valid move.
3. `place(row, col)` puts the current player's mark in that cell.
4. `place` raises `InvalidMove` when:
   - `row` or `col` is not an `int` in 0..2 (a `bool` is not accepted),
   - the cell is already taken,
   - the game is already over.
   A rejected move changes nothing: same board, same current player.
5. A player wins with three marks in a row, a column, or either diagonal.
6. `winning_line` is the three `(row, col)` cells of the winning line, in order
   from top/left to bottom/right; for the anti-diagonal the order is
   `(0, 2), (1, 1), (2, 0)`. It is `None` when nobody has won.
   The vision layer uses it to draw the strike-through.
7. The game is a draw when all nine cells are full and nobody has won.
8. `is_over` is true when there is a winner or a draw.
9. After the game is over, `current_player` stays as the player who made the last move.
10. `board` returns an immutable snapshot (tuple of tuples). Changing the caller's
    copy must not be possible, and earlier snapshots do not change after later moves.
11. `reset()` returns the game to a fresh state: empty board, "X" to move, no winner.

## Out of scope

No AI opponent, no board sizes other than 3x3, no I/O, no third-party packages.
