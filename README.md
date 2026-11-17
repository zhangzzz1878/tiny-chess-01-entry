# Tiny Chess — a 4KB chess engine

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/zhangzzz1878/tiny-chess-01-entry/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/zhangzzz1878/tiny-chess-01-entry/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A complete chess engine in a single `main.py` under 4096 bytes, written for
the [make.fun](https://make.fun) tiny-chess-01 bounty. Pure Python 3.13
standard library, no dependencies.

## How it plays

- **Board**: 0x88 array with signed pieces, Zobrist keys, incremental updates.
- **Search**: iterative deepening with aspiration windows, principal
  variation search, null-move pruning, late move reductions, check
  extensions, mate-distance pruning, transposition table (mate-score
  adjusted), killer moves and history ordering.
- **Quiescence**: captures and promotions, with full evasions when in check,
  plus delta pruning.
- **Evaluation**: material + formula-built piece-square tables, tapered
  king safety (middlegame/endgame), bishop pair, rook open files, and a
  small tempo bonus.
- **Determinism**: a fixed node budget per move — no clock, no randomness —
  so a replayed trial plays exactly the same moves.

## Running

The engine talks to the competition environment over HTTP:

```
MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3 main.py
```

It fetches each game, picks a move, and posts it back until the trial ends.

## Size

`main.py` is generated from the readable source with the kit's compress
command (`node cli/makefun.mjs compress`), LZMA payload plus a stub, and
stays under the 4096-byte limit; the whole tree stays under 8192 bytes.

## License

MIT — see `LICENSE`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=4mdg389a&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
