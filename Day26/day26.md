# Day 26 — Prior Authorization Workflow Simulator

## Overview
Built a gamified, drag-and-drop simulator of the real US healthcare Prior
Authorization (PA) workflow as a single self-contained HTML file —
Patient, Provider, and Payer lanes, four clinical scenarios, and every
required outcome type (Approval, Pend, Denial, Appeal, Peer-to-Peer
Review).

**File:** `prior-authorization-simulator.html` — vanilla HTML/CSS/JS only,
no frameworks, no CDNs, no localStorage. All state lives in memory for the
page's lifetime.

## Workflow Design
An 11-node swimlane graph spanning the three lanes:

Patient Visit → Order Created → Medical Necessity Review → Document
Collection → Submission Packet → Payer Intake → Utilization Review →
Decision → (branches to) File Appeal → Peer-to-Peer Review → Patient
Outcome.

The case token is dragged (or clicked, as an accessibility fallback) onto
the next unlocked stage at every step; required documents are dragged
individually into a "Case File" drop zone before the case can proceed.

## Scenarios (editable array at the top of the file)
1. **Lumbar Spine MRI** — Diagnostic Imaging
2. **Total Knee Replacement** — Elective Surgery
3. **Biologic Therapy for Rheumatoid Arthritis** — Specialty Pharmacy
4. **Inpatient Admission for Pneumonia** — Inpatient Admission

Each scenario carries its own required documents, necessity criteria text,
and the probabilities the decision engine uses (approval chance, necessity
pass rate, pend chance).

## Testing Notes
Rather than only reading the code, I drove the actual state machine
through a headless DOM test harness (jsdom) across 5 full playthroughs:

| Path | Result |
|---|---|
| Clean approval | ✅ Reached final screen, 100 efficiency |
| Pend → resupply documents → approve | ✅ Reached final screen, pend cycle logged correctly |
| Denial → appeal → Peer-to-Peer → overturned | ✅ Reached final screen, full timeline of 11 events |
| Denial → accept (no appeal) | ✅ Reached final "denied" screen |
| New Patient reset mid-flow | ✅ State and stats reset, new scenario fully playable |

This testing caught **two real bugs** before they shipped:
1. Several "Continue" buttons in the detail panel relied on an incomplete
   id-to-next-node map and silently did nothing for some stages.
2. A Peer-to-Peer overturn set `nextAllowed` back to the Peer-to-Peer node
   itself instead of the final Outcome node, making the case unable to
   ever reach the summary screen on that branch.

Both were fixed and re-verified with the same test harness.

## Features Built
- Progress stepper across the top (8 macro phases)
- Days Elapsed counter and live Efficiency Score (penalized for pend
  cycles, denials, and weak necessity documentation)
- Educational "Why this step matters" explanation after every step
- Confetti celebration on approval (vanilla canvas, no dependencies)
- Full workflow summary with a day-by-day timeline log and efficiency
  grade (A–D)
- Working Restart / New Patient button with a confirm guard mid-case

## Key Learnings
- Running simulated, deterministic playthroughs (forcing `Math.random`
  sequences in a test harness) surfaced state-machine bugs that code
  review alone missed — especially ones only visible on a less-common
  branch like the Peer-to-Peer overturn path.
- Modeling Pend as "request more info, then resubmit" rather than a dead
  end made the educational point about hidden PA delays land much harder
  than a simple denial would have.
- Splitting "what unlocks the next stage" (the action button result) from
  "what actually moves the case there" (drag/click on the board) keeps the
  drag-and-drop mechanic meaningful instead of decorative.
- A strict blue-and-black color constraint forced more thought into using
  borders, shadows, and saturation differences for hierarchy instead of
  just reaching for new colors.

## Screenshots
_Add screenshots here: scenario selection, document drag-and-drop, the
Pend cycle, a Denial → Appeal → Peer-to-Peer run, and the final workflow
summary with confetti._

## Technologies
HTML5 · CSS3 · Vanilla JavaScript · Canvas API (confetti) · jsdom (testing,
not part of the shipped file) · Claude AI
