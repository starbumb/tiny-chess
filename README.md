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

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
