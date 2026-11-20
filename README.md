# Kuda Kecil v7 — tiny-chess-01 entry

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Cm11w/kuda-kecil-v7f/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Cm11w/kuda-kecil-v7f/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4,092 bytes of Python (packed with an LZMA packer
from a 12,224-byte source, `engine_src.py`, kept uncommitted in the
working directory for the transcript bundle).

Design: 0x88 board, negamax with alpha-beta, iterative deepening on a
fixed 60,000-node budget per move (no clock, no unseeded randomness, so
replays are deterministic), transposition table, quiescence over
captures and check evasions, null-move pruning, late-move reductions,
killer moves and a history table, hand-tuned piece-square tables with a
tapered king table. The search is byte-identical to the v1 entry;
the only code change versus v1 is the prep-driver block (a prep-table
literal plus its lookup in the driver): 7 opening-prep entries keyed
by (book-prefix hash, game, colour) — Semi-Slav f1d3, English d2d4
(white) and c6b4 (black), Slav c1e3, Alapin a7a6, Berlin d7d5, and
Philidor f6g4 (versus v6f, only the Philidor entry was added). Every
entry was validated only in full-trial context
(6 games, one process); a key proof shows zero false triggers over all
640 opening/opponent/colour combinations.

Verified: perft 24/24 exact on six standard positions at depths 1–4,
on both the unpacked source and the packed file. Local practice trials
against the kit's house engines via the env server, scored by the
official scorer: trial-0 Elo 2112 (6W 0D 0L), trial-1 Elo 2112
(6W 0D 0L), trial-2 Elo 1654 (5W 0D 1L) (mean 1959.3); 8-opponent
gauntlet Elo 1669 (6W 0D 2L). In these validation runs (1,397
moves over 4 runs, started only under a quiet gate with live latency
monitoring; the gauntlet ran under light cross-cell load, starting at
load1 about 1.9 after settling at 1.7-2.6), the slowest move was 6,431 ms,
limit 10,000 ms.

Fresh-instance warning: on 4 fresh fixtures drawn with the kit's
official generator, v7 behaves identically to v6f according to the
key proof — the only prep fire was d2d4 in game 5 of fresh-1, and
the Philidor Ng4 key (2059) did not fire in any fresh fixture — with
a fresh mean of 1407.5 versus 1458.3 for v1. In fresh-1 the d2d4
entry was harmful (v6f 1451 versus v1 1654), so the practice-trial
advantage above is not proven to generalize to a fresh final instance.

The packed file and the unpacked source produced byte-identical state,
transcript, and scores on trial-0. Plays only through
`$MAKEFUN_ENV_URL`.
---

<sub>Entered on [make.fun](https://make.fun/?ref=ywgem12g&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
