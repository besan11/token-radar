# token-radar

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/besan11/token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/besan11/token-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar ranks pre-token protocols by implied value and shows a reader how to farm each one. It reads a sealed DefiLlama snapshot, scores every protocol with one transparent function of its TVL, seven-day growth, age with no token and chain breadth, and renders the board as a static page with a model sandbox that re-runs the scoring live.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <snapshot.json>
```

`main.ts` (Node 22, standard library only) writes `out/board.json`, `out/data.js`, `out/dashboard/`, `out/screenshots/` and `out/dossier.json`. Open `out/dashboard/index.html` in a browser to see the board; it works with no network.

## The model (radar-2)

```
implied = round( tvl_usd x 0.30
  x (1 + clamp(change_7d, -80, 200) / 100 x 0.6)
  x (0.55 + min(age_days, 1460) / 1460 x 0.45)
  x (1 + 0.03 x min(chains - 1, 5)) )
```

No protocol name is special-cased. The board covers every protocol on the snapshot's watchlist plus every rankable pre-token protocol below the watchlist floor; the live-token protocols are set aside with their market caps. Each row carries a six-step farm plan with what it costs and how long it takes.

Implied value is a model, not a price, and never a prediction that a token will launch.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
