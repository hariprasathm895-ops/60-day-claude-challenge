# Day 25 — AI Shark Tank Simulator

## Overview
Built a complete, self-contained AI Shark Tank Simulator as a single HTML
file. Users pitch a startup idea, face four distinct AI judges with their
own questions and priorities, get scored across five categories, and
receive an investment decision with valuation and reasoning.

**File:** `ai-shark-tank-simulator.html` — single file, dark Shark-Tank-style
theme, no backend, one external CDN dependency (jsPDF for the report).

## Features Built

### Startup input
Startup Name, Problem Statement, Solution, Revenue Model, Target Audience,
Funding Ask — all required before entering the tank.

### 4 AI Judges
- 🦈 **Victoria Vance, Venture Capitalist** — market size & scalability
- 🦈 **Felix Okafor, Founder** — execution
- 🦈 **Mira Chen, Customer** — usefulness
- 🦈 **Arjun Patel, Angel Investor** — profitability

Each judge asks 2 questions built from the user's own pitch details, reacts
dynamically based on answer quality, and tracks a running per-judge score
chip live during the pitch round.

### Scoring system (0–100)
Market Potential, Innovation, Business Model, Execution, and Investment
Worthiness — each computed from a heuristic engine that scores answers on
length/specificity, presence of numbers, and keyword relevance to that
judge's focus area (not random numbers).

### Investment decision
Four outcomes — **Invest**, **Reject**, **Acquire**, **Come Back Later** —
each with a suggested valuation, funding amount, and written reasoning
tied directly to the actual category scores.

### Bonus features
Confetti animation on Invest/Acquire, downloadable PDF pitch report
(jsPDF), a localStorage leaderboard (top 10, sorted by score), and a Share
Result button (Web Share API with clipboard fallback).

## Testing Notes
Rather than just eyeballing the code, I ran the engine through a headless
DOM test harness (jsdom) simulating full 8-question pitches with three
different answer qualities:

| Answer quality | Overall Score | Decision | Result |
|---|---|---|---|
| Weak/vague | 32/100 | Reject | Confirmed |
| Mediocre | 57/100 | Come Back Later | Confirmed |
| Strong, evidence-rich | 74/100 | Invest | $43,500 for 16% ($271,875 valuation) |

All four decision branches and the valuation math checked out correctly.

## Key Learnings
- "AI judges" in a backend-free single HTML file have to be simulated via
  rule-based heuristics, not real LLM calls — a static file can't securely
  call a model API on its own, so the personas are scripted but
  answer-aware rather than truly generative.
- Testing interactive logic by actually running simulated flows (not just
  reading the code) caught a real timing issue in my own test harness
  (rapid-fire dispatch bypassing a disabled button) before it could be
  mistaken for an app bug.
- Tying decision reasoning directly to the specific category scores that
  drove it (rather than generic text) makes the verdict feel earned, not
  random.
- A disabled-button guard inside the click handler itself (not just the
  UI attribute) is good defensive practice for any multi-step flow.

## Screenshots
_Add screenshots here: pitch input form, judge Q&A round with reactions,
scorecard with animated bars, decision screen with confetti, leaderboard,
and the downloaded PDF report._

## Technologies
HTML5 · CSS3 · JavaScript · jsPDF (CDN) · Canvas API (confetti) ·
localStorage · Web Share API · Claude AI
