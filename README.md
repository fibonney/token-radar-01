# token-radar-01

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/fibonney/token-radar-01/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/fibonney/token-radar-01/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

The best token launch radar: a program plus the dashboard it writes. It reads the
sealed DefiLlama snapshot, ranks every genuine pre-token launch by an implied value
derived from the snapshot's own figures, and hands a reader a farm plan for each one.

## The model (radar-2)

A protocol is rankable only when it records no token **and** is not a product of a
token that already trades: not an exchange, not a bridge, not a liquid-staking or
restaking product, not a versioned pool, and its name carries no wrapped / staked /
staking word and does not begin with an exchange's name. That is the watchlist's own
rule, applied to the whole board. Of the snapshot's 342 pre-token protocols, 144 are
set aside by it; 198 are ranked, including all 40 watchlist protocols and every
rankable protocol below the $50M floor.

Implied value, the same function for every row:

```
implied = round( tvl_usd x 0.25
  x (1 + clamp(change_7d, -60, 120) / 100 x 0.5)
  x (0.6 + min(age_days, 1095) / 1095 x 0.4)
  x (1 + 0.03 x min(chains - 1, 5)) )
```

TVL is the size of the economy a token would price; seven-day growth is the direction
it moves; age with no token is how long it has run and grown without one; chain breadth
is how widely it is already distributed. No protocol name is special-cased.

## The dashboard

- A board of all 198 ranked protocols, sortable by implied value, TVL, growth, age
  and name, with search, category and chain filters, and a watchlist-only toggle.
- A top-5 spotlight and an **early radar**: young protocols (under a year old) whose
  TVL is already growing — the launches found before the crowd.
- A detail view for each protocol: the model's four multipliers recomputed in the
  page, and a seven-step farm plan with what each step costs and how long it takes.
- A live-token view, set aside: protocols whose token already trades, shown at
  market cap, never mixed into the ranking.
- No network: every figure on the page is in `data.js`, written beside the page by
  `main.ts`. The page recomputes each row's implied value and farm plan from the
  same derivation, so the code and the board agree.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input ../input/snapshot.json
```

`main.ts` (Node 22, standard library only) reads the snapshot, writes
`board.json`, `data.js`, copies `dashboard/` and `screenshots/` to the output, and
writes `dossier.json` with the vendored `buildDossier`. Two runs write the same bytes.

## Screenshots

The three screenshots in `screenshots/` are renders of this dashboard in a headless
browser: the board, a protocol's detail view, and a filtered view.

## License

MIT, see LICENSE.

---

<sub>Entered on [make.fun](https://make.fun/?ref=cy402e4d&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
