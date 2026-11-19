# tiny-chess-01 entry

[![bounty](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/jinhongkai042-dev/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/jinhongkai042-dev/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A chess engine in under 4 KB of Python (standard library only), written for
the make.fun bounty [tiny-chess-01](https://make.fun/bounty/tiny-chess-01).

- 0x88 board, pseudo-legal move generation with castling, en passant and
  promotions, legality by king-attack test.
- Negamax alpha-beta with PVS, iterative deepening, transposition table,
  quiescence search, check extension, null move, late-move reductions,
  reverse futility pruning; moves ordered by TT move, MVV-LVA, killers and
  history.
- Tapered evaluation: material and piece-square terms kept incrementally.
  No pawn-structure terms (tested and removed because they weakened play).
- Repetitions are scored as draws, using the game's move list from the env.
- Quiescence in check searches all legal evasions and scores checkmate if none exist; repetition is scored as a draw only on the third occurrence.
- Deterministic: every search stops at a fixed node budget (200,000 nodes),
  never a clock, and uses no randomness.

`main.py` is a small loader that unpacks an LZMA payload holding the engine
source and runs it; it reads no other file.

## Run

It plays every game through the env at `MAKEFUN_ENV_URL`
(`POST /game`, `POST /move`), as the starter does:

    MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3 main.py

Grade it locally with the kit: `makefun grade-local --kit . --bot <repo>`.

MIT licence, see LICENSE.
