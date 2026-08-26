# Legends Multisport Arena — Dashboard

Live income, expense, slot utilization, breakeven, ROI and profit-distribution dashboard for **Legends Multisport Arena** (Dohar, Dhaka), built for the five partners: Galib, Asif, Siam, Priom, Mahboob.

**Live dashboard:** enable GitHub Pages on this repo (Settings → Pages → Deploy from branch `main` / root) and it will be served at:

```
https://<your-github-username>.github.io/<this-repo-name>/
```

## How it works

`index.html` is a single self-contained page. On every page load (and every 15 minutes while open) it fetches the **Sales Entry** and **Transaction Entry** tabs of the source Google Sheet directly via Google's public CSV export endpoint, and recomputes every chart, KPI and table client-side — no backend, no build step.

**Source sheet:** [Legends Dohar Sales and Expenses](https://docs.google.com/spreadsheets/d/1aVrakxcve6esM5j9LiyCX0NqJ60CG_37WvXPBcHaDcs/edit)

### ⚠️ Required: sheet sharing

For the live fetch to work for anyone (including your partners) opening the dashboard, the Google Sheet must be shared as **"Anyone with the link – Viewer"**:

1. Open the sheet → click **Share** (top right)
2. Under "General access", change to **Anyone with the link**
3. Role: **Viewer**
4. Save

If the sheet is not shared this way, the dashboard automatically falls back to a saved snapshot (as of 26 Aug 2026) and shows a banner explaining that live data couldn't be reached — it never breaks, it just goes stale until sharing is fixed.

Nothing else about the sheet changes — link-viewable means anyone with the exact URL can *view* it (not edit), same as any "share via link" you've used before. If you'd rather not make the sheet link-viewable at all, keep the dashboard on the static-snapshot fallback and ask Claude to refresh `index.html` periodically instead (a scheduled task can regenerate and push a new snapshot on a cadence you choose, without changing sheet sharing).

## What's in the dashboard

- Income vs. expense (monthly trend + expense category breakdown)
- Slot & booking analysis: utilization, demand by time of day, day of week, and a day×hour heatmap, peak vs. off-peak split, top clients
- Path to breakeven & ROI: cumulative profit vs. the ৳37,00,000 investment, two forward scenarios, annualized ROI
- Monthly profit distribution: **15% of every profitable month is reserved as a fund** for future investment/expenses; the remaining **85% is split five ways** across the partners. Loss months hold no reserve.
- AI budget-planning and growth/risk suggestions generated from the underlying data

## Updating the dashboard's design

The whole page (styles, charts, copy) lives in `index.html` — edit it directly and push, or ask Claude to make changes and push them here. The category-grouping logic for expenses (which line items count as "Maintenance", "Utilities", etc.) is in the `CAT_GROUPS` array near the top of the `<script>` block, and adapts automatically if new expense categories are added to the sheet.

## Files

- `index.html` — the live dashboard (open this, or serve via GitHub Pages)
- `README.md` — this file
