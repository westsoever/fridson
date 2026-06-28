# Fridson — Build Roadmap (What's Next to Build)

**Purpose:** A build-sequencing view of the product — what's done, what to build next, and in what order. Complements [[ACTIVE_PLAN]] (the session/phase plan).
**Source of truth:** [[06-Wiki/decisions/2026-06-27-final-commitment|Final Commitment]]
**Last updated:** 2026-06-28

> Build order follows the canonical flow: **onboard → scan → report → pinpoint → route → bid/negotiate → book → approve.** Each item lists its acceptance criteria and what it depends on. Build top-down; don't start an item until its dependencies are ✅.

---

## Legend
- ✅ Done · 🔨 In progress · ⏭️ Next · 🧊 Later (roadmap, not demo-critical)
- **Demo-critical** = must work (live or scripted) in the 3-min pitch

---

## NOW — the spine (must work for the demo)

### 1. Capture → Structured Report  ✅  *(demo-critical)*
The tenant scan→tap and the structured report object.
- **Build:** verify 5 assets, 2 distinct routes; ensure each report persists `asset · location · issue · route · timestamp`.
- **Acceptance:** scan any of 5 QR → tap issue → row appears in admin within 2s; success copy differs by route.
- **Depends on:** nothing (live at fridson.lovable.app).
- **Status:** ✅ built (capture + routing + workspace UI); verify on live after migration `20260627200000_triage_operations` applies.

### 2. Building Schematic + Location Pinpoint  🔨  *(demo-critical)*
The visual "AI knows exactly where" beat.
- **Build:** seed one floorplan image; add x/y+floor coords to the 5 assets; render a live marker on report.
- **Acceptance:** scanning `printer-3f` drops a marker on the printer's spot within ~2s; legible when projected.
- **Depends on:** #1 (report event to trigger the marker).
- **Status:** 🔨 floorplan + coords seeded; `/schematic` per-floor markers pushed `6b50e0c`; **verify pulse on live** after migrations.

### 3. Contractor/Provider Directory  ✅  *(demo-critical)*
Makes "selects 3 of 50" real.
- **Build:** seed ~50 providers (name, trade, zone, email, rate); query/filter by issue type + zone.
- **Acceptance:** a leak ticket returns ≥3 plumbing providers in-zone, ranked.
- **Depends on:** #1 (issue type + zone from the report).
- **Status:** ✅ 55 providers in migration `403ee22`; verify query on live DB after `db push`.

---

## NEXT — the agent loop (the WOW, build after the spine)

### 4. AI Property Manager: provider selection + reasoning  🔨  *(demo-critical)*
- **Build:** agent picks ~3 providers and emits a human-readable reasoning line into the activity feed.
- **Acceptance:** feed shows "Selected 3 of 50: …, because trade=plumbing, zone=2F."
- **Depends on:** #3.
- **Status:** 🔨 resolution agent built in `supabase/functions/agent/`; deploy + live verify pending.

### 5. RFQ email outreach + bid parsing  🔨  *(demo-critical, real where possible)*
- **Build:** send real RFQ emails to controlled inboxes; parse replies into comparable bids.
- **Acceptance:** ≥1 real email sent + ≥1 real reply parsed into a bid row; others may be pre-fetched (labelled).
- **Depends on:** #4 + demo vendor inboxes (optional) + **Supabase Edge** + optional **Resend** (`RESEND_API_KEY`, `AGENT_LIVE_EMAIL=1`).
- **Status:** 🔨 built with labelled stubs; real email needs secrets + deploy.

### 6. Negotiation + slot booking  🔨  *(demo-critical)*
- **Build:** one negotiation round within FM-set target/ceiling; book a repair slot (calendar hold/confirmation).
- **Acceptance:** feed shows negotiated price + "Technician booked for {date}".
- **Depends on:** #5.
- **Status:** 🔨 built in resolution agent; deploy pending.

### 7. PM Approve/Disapprove + audit log  🔨  *(demo-critical)*
- **Build:** approve/disapprove control gates the booking; log every agent step against the ticket.
- **Acceptance:** Approve confirms booking; Disapprove loops back to selection; full step log visible.
- **Depends on:** #6.
- **Status:** 🔨 workspace approve UI + agent decision API built; verify on live after deploy.

### 8. Background Activity Projection  ✅🔨  *(demo-critical — presentation layer)*
- **Build:** projection view = schematic + live feed wiring #2–#7 into one ≤60s sequence; scripted fallback.
- **Acceptance:** one scan drives the whole projected sequence with no extra clicks; readable from stage.
- **Depends on:** #2–#7 (consumes their events).
- **Status:** ✅ `/projection` built with mock ~54s timeline; 🔨 real feed (`?feed=real`) blocked on migrations + edge deploy.

---

## SUPPORTING — pitch deliverables (parallel, no heavy build)

### 9. Context & Ecosystem view  🔨  *(demo Minute 2)*
- **Build:** per-ticket context record showing ≥2 stakeholder lenses (insurer / energy / compliance); triage-shift script.
- **Acceptance:** one ticket shows multi-stakeholder value; triage-shift line ≤20s.
- **Depends on:** #1.
- **Status:** 🔨 stakeholder lens tabs in `WorkRecordPane` (Phase 5); ecosystem script in [[pitch/ecosystem]].

### 10. Business Case numbers  🤝  *(demo Minute 3)*
- **Build:** quantify cost ↓, time ↓, quality tradeoff ("80% quality + cheaper + faster = win"); one slide.
- **Acceptance:** 3 defensible numbers with stated assumptions.
- **Depends on:** [[04-Resources/Z2D/hackathon-strategy]] validation data.
- **Status:** 🤝 pitch docs drafted — [[pitch/business-case]].

### 11. Demo props + hardware  🧑  *(demo-critical, logistics)*
- **Build:** print 5 QR codes; confirm presenter, phone, projector, network.
- **Acceptance:** dry-run on real hardware succeeds.
- **Status:** 🧑 human queue — see [[pitch/logistics]] (Phase 4).

---

## LATER — roadmap (narrate as vision, do NOT build for Sunday)

- 🧊 **Real schematic/CAD import** during onboarding (demo uses a seeded floorplan)
- 🧊 **AI voice negotiation calls** (stretch headline; email is the safe core)
- 🧊 **Sensors → predictive maintenance** feeding the same loop
- 🧊 **Real insurer / energy-utility integrations** (Minute 2 is framing + mock record only)
- 🧊 **Payments / autonomous purchasing** (PM approval stays human; never autonomous spend)
- 🧊 **Multi-building / multi-tenant** management

---

## Critical path (build in this order)

```
#1 Capture ──► #2 Schematic pinpoint
   │                 │
   └──► #3 Directory ─┴─► #4 Selection ─► #5 RFQ email ─► #6 Negotiate+Book ─► #7 Approve+Audit ─► #8 Projection
```

`#9`, `#10`, `#11` run in parallel (no code dependency on the agent loop).

## Suggested ownership (3 builders)
| Track | Items | Why grouped |
|-------|-------|-------------|
| **Frontend / projection** | #2, #8, #11 | Schematic + activity feed + stage logistics |
| **Agent backend** | #3, #4, #5, #6, #7 | The autonomous loop end-to-end |
| **Pitch / business** | #9, #10 + script | Minute 2 & 3 narrative + numbers |

## Related
- [[ACTIVE_PLAN|Active Plan (phases + gates)]]
- [[plans/README|Execution plans (00–07)]]
- [[RESOLUTION-AGENT|Resolution Agent spec (detailed)]]
- [[MVP-FLOW|MVP Flow spec]] · [[LOVABLE-PROMPT|Lovable build prompt]]
- [[06-Wiki/decisions/2026-06-27-final-commitment|Final Commitment (source of truth)]]
