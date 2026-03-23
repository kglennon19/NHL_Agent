# NHL Line Scout — v2

Single-file NHL puck line + totals betting model. Deploys to GitHub Pages.

## What's New in v2

- **NHL API Tier 2 goalie scraper** — one paste on nhl.com pulls last-5 SV%, situational splits
- **Totals model** — projects total goals, surfaces OVER/UNDER lean
- **Formula recalibrated** — EV threshold 0.20g, goalie confidence discount, PDO seasonal scaling
- **~1200 lines of dead code removed** — MoneyPuck/NST/DailyFaceoff stubs, MAR14 bootstrap, duplicate API path

## Deploy

1. Upload `index.html` to [kglennon19/NHL_Agent](https://github.com/kglennon19/NHL_Agent)
2. Wait 30–60s for GitHub Pages to rebuild
3. Hard reload in incognito: `Ctrl+Shift+R`

## Data Tiers

| Tier | Source | User Action | Goalie Data |
|------|--------|-------------|-------------|
| 1 (auto) | ESPN API | None | Season SV% for confirmed starters |
| 2 (paste) | NHL EDGE API | One paste on nhl.com | Last-5 SV%, 5v5 SV%, game logs |
| Adv (paste) | Hockey Reference | One paste on hockey-reference.com | xGF%, CF%, HDCF%, PDO |

## Formula v2 Changes

- Default weights: xG 22%, Shot Quality 18%, **Goalie 28%**, PP 14%, Recency 10%, Context 8%
- EV threshold: **0.20 goals** (was 1.5 — was discarding real edges)
- Goalie confidence discount: 35% reduction for projected/unknown starters
- PDO regression scaled by `(82 - games_played) / 82`
- B2B: road 0.18g, home 0.08g (was flat 0.15g)
- Totals: crossover scoring rates + goalie suppression model
- ROI: blended puck line pricing (0.87 payout, not flat -110)
