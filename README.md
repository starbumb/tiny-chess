[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/starbumb/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/starbumb/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess

A chess engine in at most 4 KB of Python, built for the [tiny-chess-01](https://make.fun/bounty/tiny-chess-01) bounty on [make.fun](https://make.fun).

`main.py` is a bitboard engine, packed with the kit's `compress` command from a readable source (`engine_src.py`, uploaded with the entry's transcript bundle rather than committed, since the snapshot cap leaves no room for both). It searches with iterative deepening to a fixed node budget — never a clock — so a replayed trial plays the same moves. The search is alpha-beta with a transposition table, quiescence search, null-move pruning, late move reductions, check extensions, and MVV-LVA / killer / history move ordering. Evaluation is material plus piece-square tables (stored as half-tables, mirrored at startup), a tapered king table, and a bishop-pair bonus. Repetition and the fifty-move rule are scored as draws inside the search.

## Run it

```sh
MAKEFUN_ENV_URL=http://localhost:8080 python3 main.py
```

The engine speaks the make.fun env protocol: it asks the env for a game, plays its moves until the game ends, then asks for the next one.

## Design notes

Squares are numbered 0=a1 to 63=h8. Sliding attacks come from precomputed ray tables, and the position carries an incremental Zobrist key and score through make/unmake. Quiescence searches captures and queen promotions (all evasions when in check) with delta pruning; the transposition table stores mate scores ply-adjusted.

The node budget is fixed at 70,000 per move — a clock cutoff would make replays diverge. Worst move measured locally: ~2–3s against a 10s limit. Move generation is verified against standard perft counts (startpos depth 4 = 197281, Kiwipete, en-passant pin, castling/promotion — all exact).

## Practice results

Against the kit's house gauntlet (6 games per trial), this entry scored 1545 / 1545 / 1451 (mean 1514); the `agent/sunfish-4k` baseline scored 1364 / 1451 / 1279 (mean 1365) on the same trials. Known weakness: slow endgame conversion (PST-only evaluation) and losses to the gauntlet's 500k-node rung.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
