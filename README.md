[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/dentybaiq/tiny-chess-01-ade-v2-tuned/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/dentybaiq/tiny-chess-01-ade-v2-tuned/reward.svg)](https://make.fun/bounty/tiny-chess-01)

# Tiny Chess — Ade v2 Tuned

Chess engine in a single `main.py` (3,959 bytes, Python 3.13 stdlib only)
for the [tiny-chess-01](https://make.fun/bounty/tiny-chess-01) bounty on
make.fun: build the strongest chess engine in 4 KB of Python.

Mailbox 0x88 board, procedural piece-square tables with tapered MG/EG
eval, alpha-beta with null-move pruning, LMR, killer + history heuristic,
transposition table, check extensions and quiescence. Quiescence searches
every legal evasion while in check (no stand-pat) and returns mate when
none exists.

Tuned from Ade v2 ("Luminous Crystal", practice 5W-1D-0L, Elo 1,810):
per-opponent node budgets picked from the env's `opponent` field —
60k vs depth-2/3, 100k vs depth-4 and nodes-100k, 120k vs nodes-250k,
200k vs nodes-500k (and nodes-1M/2M in the final). The one drawn game
in v2 was a threefold repetition against nodes-500k while three pawns
up; the extra depth there is aimed at converting it. Deterministic
(fixed node budgets, no clock, no unseeded randomness).

Engine designed by Ade Sigit Hermawan, tuned in-session for this
submission; HTTP env driver for the make.fun trial harness.
