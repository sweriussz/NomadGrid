<div align="center">

# ☀️ NomadGrid

### AI Simulator for Off-Grid Solar Microgrids in Kyrgyzstan

A full engineering and financial calculator for solar microgrids — panels, batteries, cost, payback period, CO₂ savings — built on real 2025 Kyrgyzstan data. Runs entirely in the browser, no server, no sign-up.

🏆 **2nd Place, National Science Fair DiscoverX**

[▶ Open the Simulator](nomadgrid_main.html) · [The Problem It Solves](nomadgrid_problem.html) · [Landing Page](index.html)

</div>

---

## About

Kyrgyzstan is formally 100% electrified, but the reality in mountain villages tells a different story: **83% of households** face energy shortages in winter, and in isolated high-altitude regions less than 60% of residents get reliable grid power. The only widely available "alternative" — a diesel generator — costs **10–15× more** than the grid tariff.

**NomadGrid** answers a simple question: *how much would it cost to build an off-grid solar microgrid for a specific village in a specific region of Kyrgyzstan — and how long would it take to pay for itself?*

Instead of generic global averages, the simulator uses:
- real monthly solar irradiance data (NASA POWER) across 7 regions of Kyrgyzstan;
- official Ministry of Energy of Kyrgyzstan tariffs;
- real average rural household consumption (National Statistics Committee of KR);
- real retail prices for panels and LiFePO4 batteries on the Kyrgyz market.

## What's Inside

The project consists of three linked HTML pages:

| Page | Purpose |
|---|---|
| [`index.html`](index.html) | Landing page: the problem, key figures, overview of simulator features |
| [`nomadgrid_problem.html`](nomadgrid_problem.html) | A deep dive into the problem — a real case study, UNDP statistics, a map of regions by severity |
| [`nomadgrid_main.html`](nomadgrid_main.html) | The simulator itself — interactive map, system parameters, 8 tabs of analytics |

## Simulator Features

- **☀️ Interactive map of Kyrgyzstan** — pick one of 7 regions (Naryn, Issyk-Kul, Chuy, Talas, Jalal-Abad, Osh, Batken) by clicking the solar heatmap or from a dropdown.
- **🔋 Panel & battery sizing** — the number of 400 W panels and LiFePO4 battery capacity are sized against the worst winter month (January), with a buffer for 2 days of autonomy.
- **💰 Real 2025 KR pricing** — panels (16,000–27,000 som), batteries (~22,500 som/kWh), grid tariffs (1.64 / 2.94 som/kWh), diesel cost (~20 som/kWh including mountain delivery).
- **📊 Generation vs. demand balance** — a monthly chart accounting for seasonal demand (winter consumption runs roughly 2× higher than summer).
- **⚡ Scenario comparison** — microgrid vs. national grid vs. diesel generator, compared on cost per kWh, reliability, CO₂, and service life.
- **🏠 Outage simulation** — a visualization of houses dropping off the grid when batteries fall to 30%, with load-shedding priority and an event log.
- **🧠 10-year AI forecast** — text recommendations plus a chart of long-term energy balance, factoring in panel degradation and rising demand.
- **🎲 Monte Carlo method (1,000 simulations)** — estimates the range of possible payback periods under input uncertainty: GHI ±15%, panel price ±20%, consumption ±10%, diesel price ±25%. Outputs the median, 10th/90th percentiles, and a 90% confidence interval.
- **📐 Sensitivity analysis** — which parameter has the biggest effect on payback period when varied by ±30%.
- **🌡️ Panel thermal losses** — computes the temperature coefficient of efficiency (γ = −0.35%/°C): at −22°C in Naryn, panels produce ~16.5% more than their rated output.
- **📄 PDF report export** — a ready-made technical report with charts and recommendations, generated with a single click — suitable for a local administrator, investor, or bank.
- **🇰🇬 / 🇺🇸 Currency toggle** — som ⇄ US dollar.

## Calculation Methodology

```
Monthly panel output   = GHI(region, month) × system_efficiency × panel_area × days_in_month
Monthly demand          = houses × kWh_per_house × seasonal_coefficient(month)
Panels required          = ceil((January_demand / January_panel_output) × 1.10)
Battery capacity        = winter_daily_demand × 2 days × 1.15 (buffer)
Payback period           = system_cost / annual_savings (vs. diesel or vs. grid)
```

System efficiency accounts for inverter losses, wiring, and mismatch. Whether the model compares against diesel or the grid tariff depends on the region's winter grid reliability.

## Data Sources

| Source | What it provides |
|---|---|
| **NASA POWER · IRENA** | Monthly solar irradiance (GHI), kWh/m²/day, for each region |
| **Ministry of Energy of Kyrgyzstan** (May 2025) | Official electricity tariffs |
| **National Statistics Committee of KR** (2024) | Average rural household consumption — 232 kWh/month |
| **volta.kg, bobbystore.kg** | Retail prices for 400 W solar panels |
| **220.kg** | Retail prices for LiFePO4 batteries |
| **UNDP** (2024) | Statistics on energy poverty and power outages |
| **World Bank · AKDN** | Model validation against real-world projects (Pamir Energy, rural electrification) |

## Tech Stack

The project is deliberately built with **no build step and no backend** — three static HTML files that can be opened directly in a browser or hosted on GitHub Pages.

- Plain **HTML / CSS / JavaScript** (no frameworks)
- [Chart.js](https://www.chartjs.org/) — generation/demand, Monte Carlo, sensitivity, and thermal-loss charts
- [jsPDF](https://github.com/parallax/jsPDF) + [html2canvas](https://github.com/niklasvh/html2canvas) — PDF report generation
- Google Fonts: Unbounded, Space Mono, IBM Plex Sans

## Running Locally

No dependencies or installation required:

```bash
git clone https://github.com/<your-username>/nomadgrid.git
cd nomadgrid
```

Just open `index.html` in your browser — or, for convenience, run a local server:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

You can also deploy it with **GitHub Pages** (Settings → Pages → Source: main) and the project will be live at a direct link.

## Repository Structure

```
nomadgrid/
├── index.html               # Project landing page
├── nomadgrid_problem.html   # The problem statement page
├── nomadgrid_main.html      # The microgrid simulator
└── README.md
```

## About the Project

NomadGrid was developed as a project for the **National Science Fair DiscoverX**, where it won **2nd place**. The goal of the project is to show that solving energy poverty in Kyrgyzstan's mountain regions can be modeled precisely with real, verifiable data — not rough estimates.

---

<div align="center">
<sub>🇰🇬 Made for Kyrgyzstan · 2025</sub>
</div>
