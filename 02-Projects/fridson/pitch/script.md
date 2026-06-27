# The Locked 3-Minute Pitch Script

**Owner:** Track 4 (Pitch) · **Status:** LOCKED for Sun 16:00 demo (re-time at dry-run)
**Anchors:** [[06-Wiki/decisions/2026-06-27-final-commitment]] (canonical arc) · [[ACTIVE_PLAN]] Phases 5–7 · numbers from [[pitch/business-case]] · ecosystem from [[pitch/ecosystem]]
**Rule:** Each minute maps to its source-of-truth section. Every live beat has a tested fallback (see [[pitch/logistics]] for the recordings).

> **One-liner (say it if asked in 1 sentence):** *"Fridson is a suite of AI employees for property management — a tenant scans a broken asset, and Fridson writes the report, finds the right contractors, negotiates the price, and books the repair, while the property manager only approves."*

**Demo building:** 5 seeded assets — `printer-3f` (Printer · 3rd floor East), `bathroom-2f` (Bathroom · 2nd floor), `meeting-4f` (Meeting room · 4th floor), `pump-basement` (Pump room · Basement), `kitchen-1f` (Kitchen · Ground floor).
**Hero asset for the live scan:** `meeting-4f` → **"Projector broken"** (high-cost → triggers the full route→bid→negotiate→book agent). Backup hero: `bathroom-2f` → **"Leak"**.

---

## Setup before you speak (off the clock)
- Projection view open on the big screen (schematic + activity feed), zeroed/reset.
- Presenter phone unlocked, camera open, on the **same network**, 5 printed QR codes on the table.
- Admin/reports page open in a background tab (live backup).
- Fallback recording cued at 0:00 in a background tab (see [[pitch/logistics]]).

---

## MINUTE 1 — Live demo + narration (the product)
*Source: Final Commitment, Minute 1. Target: whole scan→approve flow visible + explained in ~60s.*

| Time | Presenter says (narration) | On screen / action |
|---|---|---|
| 0:00–0:20 | **"It's always a hassle to report problems at work. The coffee machine's broken. The printer's out of paper. A projector dies right before a meeting. What do you actually do? You shrug, send a vague email, and hope someone figures it out."** | Title slide → switch to projection view (building schematic). |
| 0:20–0:30 | **"Watch. I'm a tenant. The projector in meeting room 4 just died."** *(scan the QR live)* | Presenter scans `meeting-4f` QR with phone → scan page loads: *"Meeting room · 4th floor."* Taps **"Projector broken."** Success screen: *"Sent."* |
| 0:30–0:45 | **"That's all the tenant does — three seconds, no app, no login. Now watch what Fridson does behind them."** | Projection: marker **pinpoints** meeting room 4F on the schematic; **structured report** writes itself (asset · location · issue). |
| 0:45–1:00 | **"Fridson writes the report, locates the asset, queries 50 contractors and picks the 3 that fit, emails them for bids, negotiates the price, and books a slot — autonomously."** | Activity feed streams: *report created → 3 of 50 providers selected → RFQ emails sent → bids in → negotiated price → slot proposed.* PM view shows **Approve / Disapprove**. Presenter taps **Approve** → *"Technician booked."* |

**Beat = fallback (each live beat must survive a failure):**
- **Scan fails / camera won't focus** → presenter opens the asset URL from a bookmark (`/r/meeting-4f`); narrate as if scanned.
- **Page slow / network drops** → switch to the **pre-recorded screen capture** of the full flow (cued in background tab); keep narrating live over it.
- **Activity feed stalls** → the projection runs its **scripted timeline fallback** (Phase 4); say *"this is the same flow we just triggered."*
- **Agent step errors** (no bid / no email) → admin/reports page shows the **pre-fetched bids + pre-booked slot**; label honestly as prepared data in dry-run notes.
- **Total live failure** → play the **full 60s recording** end-to-end; pitch continues on time.

---

## MINUTE 2 — Context & ecosystem (the moat)
*Source: Final Commitment, Minute 2 + [[pitch/ecosystem]]. Framing + mock record — no real integrations.*

| Time | Presenter says | On screen |
|---|---|---|
| 1:00–1:20 | **"Reporting a hassle creates *context* — a structured, timestamped record of what failed, where, and how it was fixed. That record isn't just for the property manager."** | Show the ticket page; toggle to a second **stakeholder lens** on the same event. |
| 1:20–1:45 | **"An *insurer* gets proof-of-issue — leak detected 14:32, plumber dispatched 14:41, fixed same day. An *energy team* gets a repair-and-consumption audit on that failing pump. A *compliance* inspector gets the full audit trail in one click."** | Cycle the 3 lenses (insurer / energy / compliance) on the mock context record. |
| 1:45–2:00 | **Triage-shift line (verbatim):** *"Before Fridson, the property manager *was* the system — they triaged every vague report, called around, chased three contractors for quotes, and haggled. Now they get one notification with a negotiated recommendation and do one thing: approve, or disapprove. The orchestration runs itself."* | Split visual: "Before — PM orchestrates everything" → "After — PM approves." |

**Fallbacks:**
- **Mock context toggle breaks** → use the static **ecosystem slide** (3 stakeholder cards) and narrate the bathroom-leak example.
- This minute is narrative — **no live dependency**; it can always be delivered on slides alone.

---

## MINUTE 3 — Business case (the win)
*Source: Final Commitment, Minute 3 + numbers from [[pitch/business-case]]. ≤60s. Do not improvise numbers — read these.*

| Time | Presenter says | On screen |
|---|---|---|
| 2:00–2:15 | **"The facility-software market is $2.98 billion and growing to nearly $5 billion — but the expensive part still sits on the property manager: triaging vague reports and chasing vendors for quotes."** | Business-case slide: market frame + 3 numbers. |
| 2:15–2:35 | **"Fridson cuts that coordination cost 15 to 25% — about DKK 140 to 320 thousand a year per building, roughly half a full-time role. And it takes a high-cost repair from three-to-five days down to same-day, with a decision-ready recommendation in minutes."** | Highlight **Cost ↓** and **Time ↓** rows. |
| 2:35–2:55 | **"Is the agent as good as a veteran property manager? Call it 80%. But the human approves every cent, it costs about a fifth of traditional management, and it's far faster. 80% of the quality, cheaper, and faster — that's a win."** | Highlight **Quality** row + the "80% = win" framing. |
| 2:55–3:00 | **"Fridson: a suite of AI employees for property management. From a broken projector to a booked repair — without anyone lifting a finger."** | Close slide / logo. |

**Fallbacks:**
- **Slide deck fails** → numbers are memorized above; the three numbers + assumptions live in [[pitch/business-case]]. Deliver verbally.
- **Asked "where do these come from?"** → cite: Mordor Intelligence (market), EliseAI 15–25% / up to 80% lead-response, ERI/SalaryExpert (Copenhagen labor), TIDY 3.9% vs 20–35%. Full sources in [[pitch/business-case]].

---

## Timing budget (must total 3:00 — re-verify at dry-run)
| Section | Budget | Cumulative |
|---|---|---|
| Minute 1 — live demo + narration | 60s | 1:00 |
| Minute 2 — ecosystem + triage shift | 60s | 2:00 |
| Minute 3 — business case | 60s | 3:00 |

**Acceptance (from track plan):** end-to-end dry-run hits **exactly 3:00**; each minute maps to its source section; every live beat has a tested fallback; business-case narration ≤60s.

---

## Q&A backstops (after the 3 min)
- **"Is the AI real or scripted?"** → "The report, routing, and email RFQ are real; we label any pre-fetched data. The live call is the stretch beat with a recorded fallback." (Per [[02-Projects/fridson/RESOLUTION-AGENT]] guardrails.)
- **"Does it spend money on its own?"** → "Never. The PM approves every commitment; the agent negotiates only within FM-set bounds, with a full audit trail."
- **"How is this different from MaintainX / Snapfix?"** → "They give you a *work order*. We give you a *resolved order* — sourced, negotiated, booked. We're the coordination layer they leave on the PM's desk." (See [[04-Resources/Z2D/competitor-validation]].)
