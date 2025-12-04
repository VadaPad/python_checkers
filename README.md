# pythoncheckers

Simple console-based implementation of classic checkers in Python.

---

## Game scope

- Classic 8×8 checkers, only dark squares used.
- 12 white pieces vs 12 black pieces.
- Men move one step diagonally forward.
- Men capture by jumping diagonally over an opponent piece.
- Kings move and capture diagonally in both directions.
- Captures are mandatory; if a capture is possible, the player must capture.
- Multi-capture in one turn must continue as long as further captures are possible.
- The game ends when the opponent has no pieces or no legal moves.

---

## Data model

- `Color`: `WHITE`, `BLACK`.
- `PieceType`: `MAN`, `KING`.
- `Piece`:
  - `color: Color`
  - `type: PieceType`
- `Board`:
  - 8×8 grid storing pieces or empty cells.
  - Methods to get and set pieces and to check board bounds.
  - No turn logic or winner logic inside the board.

---

## Game logic

- `Game` holds:
  - `board`
  - `current_player`
  - `is_over`
  - `winner`
- `get_valid_moves()`:
  - Returns all legal moves for `current_player`.
  - If any capture exists, only capturing moves are returned.
  - Moves include full paths for multi-captures.
- `make_move(from_pos, path)`:
  - Validates against `get_valid_moves()`.
  - Applies the move, removes captured pieces, promotes to king if needed.
  - Switches `current_player` and updates winner state.
- `check_winner()`:
  - Decides the winner based on remaining pieces and available legal moves.

---

## Console UI

- Prints the board as a grid with coordinates:
  - Rows labeled `A–H` (or `0–7`).
  - Columns labeled `1–8` (or `0–7`).
  - Clear piece labels, e.g. `w/b` for men and `W/B` for kings, or `WP1`, `BP3`, etc.
- Shows whose turn it is.
- Displays a numbered list of all available moves and allows the player to choose by index.
- Validates user input and re-prompts on errors.
- Prints the winner when the game ends.
