# Day 27 — Prior Authorization Story Simulator

## Overview
Built a narrative, chat-based simulator that walks through a patient's
Prior Authorization journey as an 8-scene story with branching dialogue
choices — turning the same PA process from Day 26 into a character-driven
educational experience instead of a workflow board.

**File:** `prior-authorization-story-simulator.html` — single file,
Tailwind CSS via CDN, vanilla JavaScript. Strict rule: the chat feed is
append-only — every element is built with `createElement` + `appendChild`;
`innerHTML` is never set on the chat container, even on Restart.

## Characters
- 👦 **Rahul** — patient, left-aligned chat bubble
- 👧 **Priya** — healthcare operations specialist, right-aligned chat bubble
- **Dr. Patel and the narrator** — centered italic text only, never a chat
  bubble, exactly as specified

## The 8 Scenes
1. **Doctor Visit** — Rahul is diagnosed with Rheumatoid Arthritis, prescribed Humira
2. **Insurance Roadblock** — Provider submits PA directly to StarCare Health* (no pharmacy involved)
3. **What is PA?** — Priya explains it in plain language, citing the AMA 2023 PA Survey
4. **Insurance Review** — eligibility, clinical documentation, ICD-10 match, step therapy history
5. **Denial** — missing step therapy documentation; Priya notes the 2+ staff-hour cost to resolve
6. **Appeal** — gathering documentation, Letter of Medical Necessity, formal filing
7. **Approval** — reference number issued, saved on file, no repeat PA needed
8. **Takeaways** — two perspective panels: Patient (what Rahul learned) and System (denial rate, appeal rate, resolution time)

*StarCare Health is labeled an illustrative example throughout, including in the footer disclaimer.

## Choices & Branching
Two choices appear after every scene. They don't fork the overall plot,
but each one changes Rahul's actual next line — and the choice in Scene 7
("What should I take away?" vs. "How do health systems track this?")
flips the order the two Scene 8 takeaway panels appear in.

## Testing Notes
Verified with a full jsdom run clicking through all 8 scenes end-to-end:

| Check | Result |
|---|---|
| All 8 scenes advance via choice clicks | ✅ Reached "Story Complete" at 100% |
| AMA 2023 PA Survey citation present | ✅ |
| Denial and Approval banners present | ✅ |
| Both Patient + System takeaway panels render | ✅ |
| Restart clears feed without using innerHTML | ✅ Verified via `removeChild` loop, old content gone, scene 1 replays |

## Key Learnings
- An append-only DOM constraint (no `innerHTML` on the feed) is a good
  forcing function for writing small, composable render helpers
  (`addNarrator`, `addRahul`, `addPriya`, `addCard`) instead of one big
  string template.
- Letting a choice affect *presentation order* (which takeaway panel comes
  first) rather than only dialogue text is a lightweight way to make
  choices feel meaningful without building a full branching tree.
- Separating "chat bubble" (character dialogue) from "card" (status
  banners, citations, checklists) made the healthcare content much easier
  to scan than putting everything in bubbles.
- Testing the full click-through path in a headless harness caught the
  story logic working correctly end-to-end before ever opening a real
  browser.

## Screenshots
_Add screenshots here: the doctor visit scene, a choice prompt, the denial
banner, the appeal scene, the approval banner, and the final two-panel
takeaways screen._

## Technologies
HTML5 · Tailwind CSS (CDN) · Vanilla JavaScript (createElement/appendChild
only) · jsdom (testing, not part of the shipped file) · Claude AI
