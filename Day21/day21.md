# Day 21 — Digital Privacy Dashboard

## Overview
Built a premium-style cybersecurity dashboard that analyzes a sample digital
footprint (15 apps across 11 parent companies) and turns it into scores,
rankings, a risk radar, and a live privacy-improvement simulator.

**File:** `digital-privacy-dashboard.html` — single interactive HTML
artifact, Notion/Stripe/Apple-Privacy-Report inspired visual style.

## Sample Dataset (Facts)
Instagram, Snapchat, TikTok, YouTube, Discord, WhatsApp, iMessage, Spotify,
Roblox, PUBG Mobile, Amazon, Meesho, Google Search, Google Pay, Google Photos
— 15 services, 11 inferred parent companies.

## Key Results

**Digital Footprint Score: 78/100 — 🟠 Significant**
Broad presence across social, messaging, gaming, shopping and payments.

**Privacy Score: 38/100 — 🟠 Fair**
Driven down by concentration inside two ad-funded ecosystems rather than
the number of apps itself.

| Metric | Value |
|---|---|
| Total services used | 15 |
| Parent companies | 11 |
| Ecosystem concentration (top company share) | 27% (Google) |
| Estimated tracking surface | ~46 SDKs (estimate) |

## Sections Built
1. Digital Footprint Score + Privacy Score (circular gauges, color-banded)
2. Exposure Heatmap — 8 data categories × 6 most-exposed companies
3. Company Exposure Ranking — all 11 companies, ranked by exposure index
4. Data Collection Matrix — 15 apps × 8 permission categories
5. Risk Radar — 6-axis radar chart (financial, social, behavioral,
   communication, location, identity)
6. Digital Twin Profile — estimated lifestyle/demographic sketch
7. WOW Insights — surprising cross-cutting findings
8. Most Valuable Data Assets — ranked by commercial data value
9. Privacy Improvement Simulator — live-recalculating checklist that moves
   the score from Fair toward Good as actions are toggled
10. Final Verdict — plain-language summary

## Privacy Findings
- **Google and Meta together drive ~40% of total estimated exposure**,
  despite being only 2 of 11 parent companies — by far the most concentrated
  risk in the dataset.
- Google is the only company in the stack with reach into both **payments**
  (Google Pay) and a **biometric photo library** (Google Photos) — a
  combination no other single company in this footprint has.
- The single highest-leverage fix: reducing ad personalization and
  cross-app tracking inside Google and Meta. The simulator shows this can
  realistically move the Privacy Score from Fair into the Good range.
- Communication privacy risk scored lowest among the 6 risk-radar axes (46),
  largely because WhatsApp and iMessage are end-to-end encrypted by default.

## Design Rules Followed
- Every behavioural/demographic/lifestyle claim is explicitly tagged
  **Estimate**, never stated as fact
- No claim of access to private databases anywhere in the report
- Scores and rankings are calculated only from the 15 listed Facts

## Learnings
- Separating "Fact" vs "Estimate" as a visible UI tag, not just a caveat
  in prose, makes a privacy report feel trustworthy instead of alarmist.
- A small set of color-coded score bands (🟢🟡🟠🔴) communicates risk faster
  than raw numbers alone.
- An interactive simulator turns a static report into something actionable
  — seeing the score move in response to your own choices lands very
  differently than reading a list of recommendations.
- Concentration (how few companies dominate your exposure) is a more
  useful privacy signal than raw app count.

## Screenshots
_Add screenshots here: score gauges, exposure heatmap, company ranking,
risk radar, digital twin profile, and the simulator in action._

## Technologies
HTML5 · CSS3 · JavaScript · SVG (gauges + radar chart) · Claude AI
