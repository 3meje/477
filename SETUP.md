# Quick Setup — Deriv Smart Trader Pro v1.6

## 1. Get Deriv API token
https://app.deriv.com/account/api-token

Create with scopes: **Read + Trade + Payments**

---

## 2. Push to GitHub

```bash
git init && git add . && git commit -m "v1.6 release" && git branch -M main
git remote add origin https://github.com/<user>/deriv-smart-trader-pro.git
git push -u origin main
```

---

## 3. Enable GitHub Pages

Settings → Pages → Source: **main / root** → Save

URL: `https://<user>.github.io/deriv-smart-trader-pro/`

---

## 4. Login & use

- Paste your API token → **Connect & Authenticate**
- Select a market from the left sidebar (defaults to Volatility 100)
- Switch to **Higher / Lower** to reveal the barrier offset panel
- Payout preview updates live as you adjust barrier, stake, or duration
- Manual trade: **▲ Rise / ▼ Fall** (or **▲ Higher / ▼ Lower**) buttons pinned at sidebar bottom

---

## 5. Auto Trader

The Auto Trader button is pinned in the sidebar footer, below the manual trade buttons.

| Step | Action |
|---|---|
| 1 | Click **Auto Trade** to enable — button turns **green** (watching) |
| 2 | AI waits for a ≥80% confidence signal — button turns **amber** (armed / Stage 1) |
| 3 | On the next tick where confidence = 100% **AND** the last closed 1m candle is a perfect bear/bull — trade fires automatically |
| 4 | Auto trade cooldown until next candle closes, then watching resumes |

**To stop:** click the button again at any time. Resets fully on market switch.

**Perfect candle:** body ≥70% of high–low range, no wick >15% of range, direction matching the signal.

---

## 6. 1-Minute Candle Panel

Displayed as a 72px column fixed to the right side of the main price chart.

- Shows the **current forming candle** (large, highlighted)
- Shows the **last 5 closed candles** for context
- Displays: direction (▲ BULL / ▼ BEAR), body %, and ✓ PERFECT or ⚬ forming status
- Updates on every tick

---

## 7. Layout controls

| Control | How |
|---|---|
| Resize sidebar | Drag right edge of left panel |
| Resize chart vs sub-charts | Drag the handle between main chart and MACD/AO/RSI |
| Toggle indicators | Buttons in the indicator toolbar above the chart |
| Force AI re-analysis | Click **⟳ Analyse** in the signal bar |
| Switch theme | Click **☀ / 🌙** in the topbar |

---

## 8. Theme

| Setting | Detail |
|---|---|
| Default | Auto-detects OS `prefers-color-scheme` |
| Dark | Deep charcoal, sky-blue accent, teal/rose signals |
| Light | Clean white, ink-blue accent, emerald/crimson signals |
| Persistence | Saved to `localStorage` |

---

## 9. Troubleshooting

| Problem | Fix |
|---|---|
| Auth failed | Token needs Read + Trade + Payments scopes |
| No prices | Use Synthetic Indices — available 24/7 |
| Barrier panel not showing | Switch to **Higher/Lower** contract type |
| Payout shows `…` | Adjust barrier or stake to trigger proposal refresh |
| Chart blank | Wait 2–5 ticks after selecting a market |
| Auto trade not firing | Ensure confidence reaches 100% AND the last closed 1m candle is perfect |
| WebSocket error | Try the alternative Binary server in the login dropdown |
| Theme not saving | Check `localStorage` is not blocked by browser privacy settings |
