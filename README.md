# Deriv Smart Trader Pro

AI-powered trading platform for [Deriv.com](https://deriv.com). Runs entirely in your browser — no server, no build step, single HTML file.

---

## Deploy to GitHub Pages

```bash
git init
git add .
git commit -m "v1.6 release"
git branch -M main
git remote add origin https://github.com/<username>/deriv-smart-trader-pro.git
git push -u origin main
```

Then: **Settings → Pages → Source: main / root → Save**

Live at: `https://<username>.github.io/deriv-smart-trader-pro/`

---

## Get Your Deriv API Token

1. Log in at [app.deriv.com](https://app.deriv.com)
2. **Account Settings → API Token → Create new token**
3. Scopes: **Read + Trade + Payments**
4. Paste the token into the login screen and click Connect

---

## Features

- Live WebSocket price feed (Deriv API v3)
- Synthetic Indices (24/7), Forex, Crypto, Baskets, Metals
- Rise/Fall and Higher/Lower contracts
- **Barrier offset control for Higher/Lower** — live constraints from `contracts_for` API, presets at 1/2/5/10/20/50 pips, absolute price display, +/− toggle, debounced live payout proposal
- Live payout preview from real Deriv proposal API
- Charts: EMA 5/20, SMA 50, Bollinger Bands, MACD, Awesome Oscillator, RSI
- **1-minute candle panel** — live forming candle + last 5 closed candles displayed beside the main chart, with body% and PERFECT/forming indicator
- **AI signal analyser** — multi-factor confluence scoring (EMA cross, MACD, AO, RSI, price trend)
- **Auto Trader** — 2-stage AI-driven execution engine (see below)
- Open contracts, trade history, win/loss stats, performance bar chart
- Compact all-in-one layout — resizable sidebar, chart drag-handle resize
- Light & Dark mode — ☀/🌙 toggle, localStorage persistence, OS preference detection
- Optimised font clarity across all UI zones

---

## Auto Trader — 2-Stage Logic

The Auto Trader sits pinned at the bottom of the sidebar beneath the manual trade buttons.

```
Stage 1 — ARM
  AI confidence ≥ 80% in a clear direction
  → Button turns amber + pulses
  → Status: "STAGE 2 — waiting"

Stage 2 — FIRE
  Same direction + AI confidence = 100%
  AND last closed 1-minute candle is PERFECT in the matching direction
  → Trade executes immediately
  → Cooldown until next candle closes
```

**Perfect candle definition:**
- Body occupies ≥ 70% of total high–low range
- Neither wick exceeds 15% of range
- For LOWER/FALL entry: must be a perfect **bear** candle (close < open)
- For HIGHER/RISE entry: must be a perfect **bull** candle (close > open)

**Safety rules:**
- If direction flips between Stage 1 and Stage 2 → auto-disarms with warning toast
- One trade per candle — cooldown resets when the next 1-minute candle closes
- Resets cleanly on market switch and logout
- All existing AI confluence conditions (EMA, MACD, AO, RSI, trend) remain active

**Button states:**

| State | Colour | Meaning |
|---|---|---|
| OFF | Grey | Disabled |
| Watching | Green pulse | ON — waiting for ≥80% Stage 1 signal |
| Armed | Amber pulse | Stage 1 triggered — waiting for 100% + perfect candle |

---

## Layout (v1.6)

```
┌───────────────────────────────────────────────────────────────────┐
│  DSP │ ticker tape ················· │ Bal │ ID │ ● │ ☀ │ Logout │
├──────────┬──────────────────────────────────────┬─────────────────┤
│ Market   │  [Indicators toolbar]                │ Open/History    │
│ Contract │  ┌────────────────────────┬────────┐ │ Stats/AI tabs   │
│ Duration │  │   Main Price Chart     │ 1m ▼   │ │                 │
│ Barrier  │  │                        │ candle │ │                 │
│ Stake    │  ├──── drag handle ───────┴────────┤ │                 │
│ Preview  │  │ MACD  │  AO  │  RSI             │ │                 │
│ ──────── │  └──────────────────────────────────┘ │                 │
│ ▲ Rise  │  [⬡ Signal bar + Analyse btn]        │                 │
│ ▼ Fall  │                                      │                 │
│ ──────── │                                      │                 │
│ ⬡ AUTO  │                                      │                 │
│ [status] │                                      │                 │
└──────────┴──────────────────────────────────────┴─────────────────┘
```

---

## Bug Fix / Change History

| Version | Change |
|---|---|
| v1.6 | Auto Trader — 2-stage AI execution engine with 80%→100% confidence + perfect 1m candle gate |
| v1.6 | 1-minute candle panel beside main chart — live forming candle, last 5 history, body% and PERFECT indicator |
| v1.6 | Perfect candle logic — body ≥70% of range, wicks ≤15%, direction-matched to trade signal |
| v1.6 | Auto trade cooldown per candle, direction-flip disarm, clean reset on market switch/logout |
| v1.5 | Increased font sizes across all UI zones for maximum clarity |
| v1.5 | Light & dark mode with full token palette, smooth transitions |
| v1.5 | Theme persists via localStorage; auto-detects OS `prefers-color-scheme` |
| v1.4 | Compact all-in-one layout: fixed topbar, resizable sidebar, chart drag handle |
| v1.4 | Trade buttons pinned to sidebar footer |
| v1.3 | Higher/Lower barrier offset panel with live `contracts_for` API constraints |
| v1.3 | Live payout preview from real Deriv proposal API |
| v1.2 | Fixed fatal `signal` variable SyntaxError |
| v1.2 | Fixed missing `handleProposal`, stale closure, tick subscription tracking |

---

## Disclaimer

Educational and personal use only. Trading involves significant risk of loss. AI signals and the Auto Trader do not guarantee profit. Always test on a demo account first.

## License

MIT
