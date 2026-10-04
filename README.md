# Gesture Tic-Tac-Toe

Two-player tic-tac-toe played with hand gestures through a webcam.

- One hand in frame: draw your mark freehand in a cell.
- Two hands in frame: pinch to zoom the grid bigger or smaller.

Built with Python, OpenCV, and MediaPipe.

## Status

| Part | State |
|------|-------|
| Game rules engine (`tictactoe/game.py`) | In progress |
| Webcam capture and hand tracking | Not started |
| Pinch-to-zoom grid | Not started |
| Freehand drawing | Not started |

## Layout

```text
tictactoe/      game rules (no camera code)
tests/          pytest contract tests for the rules
docs/           specs
```

## Development

```bash
python -m venv .venv
.venv\Scripts\activate        # Windows
pip install -r requirements-dev.txt
python -m pytest
```

The rules are specified in [docs/game-logic-spec.md](docs/game-logic-spec.md).
