# Soul Tournament

A single-player, endless, **play-money** slot machine. Five reels, five paylines,
wild kunai, and a free-spin bonus round where every win is doubled. There is no
real-money gambling anywhere in this project.

Dark-fantasy look: a storm-lit ruined arena, gold-framed warrior symbols, hot
crimson wild and bonus marks.

## Play it

- **Live:** https://soul-tournament.higgsfield.app (sign in with Higgsfield)
- **Locally:** see *Run it* below

## Run it

The game is one Cloudflare Worker (React 19 + TanStack Start, SSR).

```bash
cd app
bun install
bun run dev      # local server
bun run test     # 48 tests: the rules, and the room over real WebSockets
bun run build    # what CI runs: logic check -> typecheck -> bundle
```

The game rules are six pure functions in `app/src/logic.js`: `meta`, `setup`,
`validateAction`, `applyAction`, `isGameOver`, `viewFor`. The screen is
`app/public/index.html` + `client.js`.

## The machine's numbers

| Metric | Value |
| --- | --- |
| Return to player | 90.1% |
| Hit frequency (any win) | 25.8% |
| Bonus round frequency | 5.5% (about one per 18 spins) |
| Bet ladder | 10 / 20 / 50 / 100 / 200 / 500 |
| Jackpot (five wilds on a line) | 10,000 |

Measured by driving the real `logic.js` head-less over 500,000 spins.

## Paytable - credits per payline at a total bet of 10, scaled by your bet

| Symbol | 3 | 4 | 5 |
| --- | --- | --- |
| Wild (kunai) | 10 | 64 | 320 |
| Champion | 8 | 40 | 160 |
| Sorceress | 6 | 32 | 128 |
| Monk | 5 | 24 | 96 |
| Assassin | 4 | 19 | 80 |
| Scroll | 2 | 8 | 32 |
| Coin | 1 | 4 | 16 |

Three or more Bonus dragons anywhere (they pay nothing on a line) start free
spins: 3 -> 10, 4 -> 15, 5 -> 20. Consecutive winning spins build a combo worth
up to +50% on the next win.

## Design notes

The design artifacts live in `design/`: `plan.md` (profile, laws, concept,
system map, verification runs), `thresholds.md` (numeric gates fixed before the
checks were designed), `assets.csv` (every visual and audio asset), and
`external_review.md` (the questions code cannot answer).

All art is original: eight warrior symbols and an arena background, generated
against one frozen style formula, then colour-keyed to transparency. Sound is
four effects plus a music loop.

**Play money only - no real-money gambling.**