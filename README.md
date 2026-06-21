# JC Citi Bike — Distribution Management Dashboard

Streamlit dashboard for the **Distribution Management** module of the JC/Hoboken Citi Bike rebalancing system. Visualises truck routes, costs, and bike movement analytics for May 2026.

## Pipeline

```
Demand Forecasting → Inventory Management → Transportation Optimisation → [Distribution Management]
```

This module is the final step: it routes all bike-movement tasks from the optimisation layer into physical truck routes using a four-phase CVRP-PD solver (Clarke-Wright + 2-opt + Or-opt + PDP stop ordering).

## How to use

**Step 1 — Generate the data**

Run `distribution_management.ipynb` locally. It produces 5 CSV files:

| File | Description |
|------|-------------|
| `distribution_routes.csv` | One row per truck route |
| `distribution_summary.csv` | One row per review window |
| `distribution_route_stops.csv` | One row per truck stop |
| `distribution_depot_deliveries.csv` | Depot-to-station delivery tasks |
| `jc_station_master.csv` | Station coordinates (from optimisation notebook) |

**Step 2 — Upload and explore**

Open the app, upload all 5 files in the sidebar, then select a date and review window (3 PM or 10 PM) to explore:

- 🗺️ Interactive truck route map
- 📋 Route summary with cost breakdown per truck
- 🔍 Stop-by-stop drill-down for each truck
- 📈 Monthly overview — trucks, cost, bikes, route durations
- 📦 Task type breakdown (S→S / D→S / S→D)

## Run locally

```bash
pip install -r requirements.txt
streamlit run distribution_app.py
```

## Deploy on Streamlit Cloud

1. Fork or clone this repo to your GitHub account
2. Go to [share.streamlit.io](https://share.streamlit.io) → **New app**
3. Select this repo → branch `main` → main file: `distribution_app.py`
4. Click **Deploy**

## Key results — May 2026

| Metric | Value |
|--------|-------|
| Review windows | 61 active (31 days × 2 shifts) |
| Trucks dispatched | 249 |
| Bikes repositioned | 5,211 |
| Total road distance | 7,397.7 km |
| Total logistics cost | $19,039.51 ($3.65 / bike) |
| Schedule compliance | 100% |

## Tech stack

| Library | Use |
|---------|-----|
| Streamlit | App framework |
| Pandas | Data wrangling |
| Plotly | Charts |
| PyDeck | Route map |

## References

- Clarke & Wright (1964). *Operations Research*, 12(4), 568–581.
- Lin (1965). *Bell System Technical Journal*, 44(10), 2245–2269.
- Potvin & Rousseau (1995). *INFORMS J. Computing*, 7(4), 443–449.
- Schuijbroek, Hampshire & van Hoeve (2017). *EJOR*, 257(3), 992–1004.
