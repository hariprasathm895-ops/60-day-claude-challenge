# Day 17 — Vehicle Cost Analysis Dashboard

## 🎯 Goal
Build a single-file HTML dashboard that compares running cost, CO₂ output, and maintenance across five fuel types (Petrol, Diesel, CNG, E85, EV), and dig into the "E85 paradox" — a fuel that's cheaper at the pump but not necessarily cheaper to drive.

## 🚗 Setup
| Field | Value |
|---|---|
| Vehicle | Maruti Suzuki Swift |
| Fuel | Petrol |
| Usage | Mixed (city + highway) |
| KM/month | 1000 |
| Car age | 3 yrs |

> Note: No real CSV was available for this run, so a synthetic-but-realistic dataset (260 rows, 5 fuel types × 13 age groups) was generated to match the schema the prompt expects: `Fuel_Type, Vehicle_Age_yrs, Distance_km, Fuel_Cost_INR, CO2_emitted_kg, Maintenance_Cost_INR, Refuel_Recharge_time_min, Fuel_Price_INR_per_unit, Mileage_km_per_unit`. Swap in a real CSV and the same HTML recomputes everything live in the browser — no numbers are hardcoded.

## 🛠️ Build
- Single HTML file — no frameworks, no CDN
- All charts hand-built in raw SVG: bar chart, doughnut, multi-line chart, semicircle gauge
- All metrics (cost/km, CO₂/km, maintenance/km, age buckets, E85 pump-saving / running-penalty / break-even, E85 score) computed client-side in vanilla JS from the embedded dataset
- Dark navy (#0a0f1e) glassmorphism theme; fixed fuel color coding — Petrol blue, Diesel grey, CNG green, E85 amber, EV purple
- Responsive from 375px to 1440px

## 📊 Key findings
- **Cost/km ranking:** EV (₹1.55) < CNG (₹3.56) < Diesel (₹4.62) < Petrol (₹6.32) < E85 (₹6.96)
- **The E85 paradox confirmed:** E85 is ~16% cheaper per litre than Petrol at the pump, but its lower energy density means ~10% *higher* cost per km once you actually drive it.
- **E85 break-even price:** E85 would need to drop to roughly ₹77/L (vs today's ~₹86/L) to match Petrol's running cost — it isn't there yet.
- **E85 Score: ~2.5/10** — it loses heavily on the cost weighting (4pts) and picks up most of its points from refuel speed, since refuelling is as fast as Petrol/Diesel and far faster than EV charging.
- **Aging effect:** Maintenance/km climbs steadily with vehicle age across every fuel type, but the slope is steepest for Diesel — its low running cost erodes faster than Petrol's as the car gets older.
- **EV's real edge isn't just running cost** — it also has the lowest maintenance/km of all five (no engine wear costs), at the expense of by far the longest recharge time (~44 min avg vs ~5–8 min for liquid/gas fuels).

## 💡 Learnings
- Computing "per-km" metrics correctly requires aggregating totals first (Σcost / Σdistance) rather than averaging individual cost/km values — averaging ratios directly would have skewed the result toward lower-distance trips.
- A "paradox" metric (E85) is much more convincing when you show all three numbers together — pump saving %, running penalty %, and break-even price — rather than just one of them in isolation.
- Pure-SVG charts (no chart library) force you to think in coordinate math (`stroke-dasharray` for the doughnut and gauge, manual x/y scaling for the line chart) — slower to build than a charting library, but zero dependencies and full control over hover tooltips.

## 📁 Files in this folder
- `day17_dashboard.html` — the full interactive dashboard
- `vehicle_cost_data.csv` — dataset used (synthetic, see note above)
- `linkedin_post.png` — share graphic for LinkedIn
- `screenshots/` — dashboard screenshots *(add your own screenshots here before committing)*

## 🔗 Day 17 commit
*(add your GitHub commit URL here after pushing)*
