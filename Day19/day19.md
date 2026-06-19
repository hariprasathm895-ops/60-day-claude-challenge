# Day 19 — Football Intelligence Hub

## Overview
Built a multi-stage AI experience using Claude that turns a personal football
workbook into a calibrated knowledge assessment and a live FIFA World Cup 2026
prediction report.

**Source data:** `football_workbook_messi.pdf` — a personal Messi-focused
training log (player profile, basic football quiz, skills practice log, match
analysis, fitness tracker, self-evaluation). Not a full tournament stats sheet,
so live World Cup 2026 data was used alongside it for the prediction stage.

## Stage 0 — Knowledge Level Check
Selected: **Casual viewer**
Used to calibrate explanation depth and terminology for every later stage.

## Stage 1 — FIFA World Cup 2026 Prediction Report
Tournament is live (group stage in progress as of the report date).

| Prediction | Pick | Confidence |
|---|---|---|
| Winner | France | 35% |
| Runner-up | Spain | 25% |
| Dark horse | Morocco | 20% |

**Player to watch:** Lionel Messi (Argentina) — scored a hat-trick in
Argentina's opening 3–0 win over Algeria, chasing back-to-back titles at 36
years old.

Each prediction included supporting evidence, key risks, and factors working
against it (e.g. France's history of slow starts, Spain's opening draw vs
Cape Verde, Morocco's thinner squad depth for a long run).

## Stage 2 — Football IQ Quiz
5 mixed-difficulty questions (beginner → advanced), covering basic rules,
World Cup format, 2022 final history, and live 2026 tournament awareness.

**Score: 4/5 correct → Football Awareness Score: 80/100**
**Classification: Football Follower**

- Strongest area: current tournament awareness + knockout-stage history
- Weakest area: new 48-team format / advancement structure
- Key gap: structural rules knowledge despite solid match-result knowledge

## Stage 3 — Messi vs Ronaldo Personality Match
12-question personality assessment (ambition, discipline, leadership,
teamwork, creativity, competitiveness, confidence, work ethic, learning
style, decision-making, pressure handling, goal-setting style) — designed to
run without ever asking a direct Messi-vs-Ronaldo question.

*Status: prompt staged and ready; full run + archetype scoring to be
completed in a follow-up session.*

## Final Output — Football Intelligence Profile
Generated profile card combining the score, classification, and World Cup
prediction summary (see screenshot).

## Key Learnings
- A single staged prompt can run an entire experience — calibration,
  analysis, assessment, synthesis — without writing app logic by hand.
- Predictions are only credible with evidence + risks attached to the
  confidence score, not just a number.
- Quizzes that adapt to a stated skill level feel personalized rather than
  generic.
- Real-time sports data turns a "static" prompt into something genuinely
  live and dynamic.
- Working with imperfect, real-world data (a personal training log instead
  of a stats workbook) is its own useful exercise.

## Screenshots
_Add screenshots of the Knowledge Check, Prediction Report, Quiz results,
and Football Intelligence Profile card here._

## Technologies
Claude AI · Prompt Engineering · Data-Driven Analysis
