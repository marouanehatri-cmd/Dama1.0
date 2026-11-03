# Dama Master — Universal Checkers Solver ♛

Single-file checkers/dama solver implementing **Moroccan Dama rules**:

- Men move 1 step diagonally **forward**; capture forward **and backward**
- **Mandatory capture** with the **MAX capture rule** (longest path forced) — `findMaxCaptureLength()`
- Flying kings (bishop-like): land on any empty square beyond the captured piece, chained captures
- Promotion ends the turn immediately, even if the new king could keep capturing
- Engine: `getAllCaptures()` (recursion + backtracking), `getAllMoves()`, minimax with α-β pruning (depth 1–15)

## Features
- Play vs engine (White or Black), or 2-player analysis board
- Variant dropdown (Moroccan max-capture / International any-capture), who starts, depth slider 1–15
- Analyze: lists **all** possibilities sorted with evaluations, capture counts and a **BEST** badge + arrow highlight
- Capture rule toggle: mandatory, or optional with the **huffing** rule (remove the piece that should have taken, or ignore it)

## Run
Open `index.html` in any browser. No build, no dependencies, fully offline.

## Test position
White king d4, Black men e5 & f6, White to move → press **Test Position** then **Analyze**: White wins by force by capturing both men.
