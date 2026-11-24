# Tiny Chess — Tuned Engine

[![make.fun bounty](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/dentybaiq/tiny-chess-01-ade-v2-tuned/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/dentybaiq/tiny-chess-01-ade-v2-tuned/reward.svg)](https://make.fun/bounty/tiny-chess-01)

Entry for the [tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01): a
small, deterministic chess engine that plays a six-game gauntlet against the
house anchors (depth-2, depth-3, depth-4, nodes-100k, nodes-250k, nodes-500k),
weakest first, and the eight-game final against the stronger anchors as well.

## How it plays

The engine uses a 0x88 mailbox board and a plain alpha-beta search with
principal-variation search, late-move reductions, null-move pruning, a
transposition table, and check extensions. Its quiescence search covers
captures and promotions, and — when the king is in check — it searches every
legal evasion instead of standing pat, returning a mate score when no evasion
exists. Evaluation is material plus tapered middlegame/endgame piece-square
tables and a bishop-pair bonus, with the game phase derived from non-pawn
material. Move ordering combines MVV-LVA captures with killer moves and a
history heuristic.

## Per-opponent node budgets

Search is bounded by a fixed node budget per move, never by wall-clock time,
so the same position and the same budget always produce the same move. The
budget is chosen from the opponent announced by the game server:

- depth-2 and depth-3: 80,000 nodes
- depth-4 and nodes-100k: 150,000 nodes
- nodes-250k: 200,000 nodes
- nodes-500k, nodes-1M, nodes-2M: 250,000 nodes
- any other opponent: 100,000 nodes

The small budgets on the weak anchors keep the average move near three
seconds (the limit is ten seconds per move). The 250,000-node budget against
nodes-500k is what converts the old trial-0 draw — a threefold repetition
while three pawns up — into a win by checkmate.

## Files

- `main.py` — the whole engine, self-contained, standard library only.
- `LICENSE` — MIT.
