# Day 18 — Custom Skill: brain-dump-action-planner

## 🎯 Goal
Build a reusable Claude Custom Skill that turns messy notes, meeting transcripts, voice memo dumps, or brainstorming sessions into a structured, interactive HTML dashboard — without inventing or assuming any information not present in the source text.

## ⚙️ Skill Setup
| Field | Value |
|---|---|
| Skill Name | `brain-dump-action-planner` |
| Trigger | Paste any messy note / transcript / brain dump and ask Claude to break it down |
| Output | Self-contained interactive HTML artifact (Notion/Linear/Asana-style dashboard) |
| Core rule | Never invent, assume, predict, or fill gaps — missing info is shown as "Not specified" |

Created once under Settings → Skills → Custom Skills, with the Name, Description, and Instructions pasted in exactly as specified. After saving, the skill can be invoked in any new conversation just by referencing it — the full instruction block never needs to be re-pasted.

## 🧪 Testing — 3 input formats, 3 modes
No real meeting notes were available for this run, so three realistic synthetic inputs were used to cover the modes the skill defines:

1. **Full Breakdown Mode** — a raw, unstructured brain-dump of an AvenoraHub sprint-planning call (names, dates, ₹ figures, an unresolved DB decision, a parked feature idea).
2. **Transcript Mode** — a speaker-labeled voice-memo transcript of a Team Yudhistra standup call (Hari / Mentor Arjun / Sneha) on Scanly's face-recognition progress, including a date discrepancy between speakers.
3. **Merge Mode** — two teammates' separate personal notes from the *same* AvenoraHub call (Hari's notes vs Priya's notes), deliberately containing overlapping tasks with conflicting deadlines.

## 📊 What the dashboards surfaced
- **Full Breakdown:** correctly separated 6 action items, 5 open questions (quiz module owner, DB choice, meeting day, privacy policy page, PPT owner), 3 risks/blockers, and 1 genuine conflict (MySQL vs Firebase) — without inventing a deadline for the API fix (left as "ASAP," not converted to a date) or an owner for the onboarding doc (shown as "Not specified").
- **Transcript Mode:** attributed decisions and action items to the correct speaker, used an "Attribution Notes" section for the one item nobody owned (the PPT update), and correctly flagged the 29th-vs-30th demo-date mismatch as a Conflict rather than silently picking one.
- **Merge Mode:** identified all 3 overlapping tasks across both notes as Duplicate Items, laid out each conflicting deadline side-by-side by source in a Conflict Resolution Review section, and left every conflict unresolved for manual decision — exactly as instructed, with a Source Information section crediting both note-takers.

## 💡 Key learnings
- The "never invent" constraint is the hardest part to get right — it's tempting for a model to round "ASAP" into a date or guess an owner from context. Explicitly requiring "Not specified" as the fallback (rather than leaving fields blank) makes missing data visually obvious instead of easy to skim past.
- Conflicts and Open Questions are easy to mix up — a conflict needs *two contradicting statements*; an unresolved single point with no stated answer is an open question, not a conflict. Defining both sections explicitly in the skill instructions prevented that blending.
- **Reusability confirmed:** none of the formatting rules, section names, badge emoji, or "never invent" constraints had to be re-typed for the 2nd or 3rd test — saving the skill once and invoking it by name reproduced the exact same structure across three very different input formats (brain-dump, transcript, merged notes).
- Merge Mode benefits from keeping a literal source tag (e.g. "Hari's Notes" / "Priya's Notes") next to every merged item — without it, the Conflict Resolution Review section loses its credibility as a side-by-side comparison.

## 📁 Files in this folder
- `day18_dashboard_fullbreakdown.html` — Full Breakdown mode test (AvenoraHub sprint call)
- `day18_dashboard_transcript.html` — Transcript mode test (Team Yudhistra standup)
- `day18_dashboard_merge.html` — Merge mode test (two conflicting note sources)
- `screenshots/` — Skill creation screen + dashboard screenshots *(add your own screenshots here before committing)*

## 🔗 Day 18 commit
*(add your GitHub commit URL here after pushing)*
