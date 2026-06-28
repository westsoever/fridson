# Demo Logistics, Submission & Open Decisions

**Owner:** Track 4 (Pitch) · **Status:** Live checklist through Sun 16:00
**Anchors:** [[ACTIVE_PLAN]] Phase 7 · [[06-Wiki/decisions/2026-06-27-final-commitment]] · script in [[pitch/script]].
**Deadlines:** Milestone 2 submission **Sun 28 Jun 15:00** · Team dry-run before **16:00** · Live demo & judging **16:00**.

**Agent-prepared docs (Phase 4):** [[pitch/qr-codes]] · [[pitch/milestone-2-copy]] · [[pitch/dry-run-checklist]]

---

## A. Demo prop / hardware checklist (🧑 human)

- [x] **QR asset doc ready** — URLs + print spec in [[pitch/qr-codes]] ✅
- [ ] **Print 5 QR codes** — one per seeded asset, on the table as props:
  - *🧑 **Ready to run:** Open [[pitch/qr-codes]] → generate 5 PNGs from the URL table → print ≥8×8 cm black-on-white → label each prop → test scan from ~30 cm on presenter phone.*
  - [ ] `printer-3f` → `/r/printer-3f` (Printer · 3rd floor East)
  - [ ] `bathroom-2f` → `/r/bathroom-2f` (Bathroom · 2nd floor)
  - [ ] `meeting-4f` → `/r/meeting-4f` (Meeting room · 4th floor) — **hero asset for live scan**
  - [ ] `pump-basement` → `/r/pump-basement` (Pump room · Basement)
  - [ ] `kitchen-1f` → `/r/kitchen-1f` (Kitchen · Ground floor)
- [ ] **Presenter confirmed** — one person drives phone + narration (decide who; default the most rehearsed).
  - *🧑 **Ready to run:** Team standup — assign one presenter (phone + narration). Write name here: ___________
- [ ] **Phone ready** — unlocked, camera app primed, brightness up, notifications off, asset URLs bookmarked as scan-fallback.
  - *🧑 **Ready to run:** On presenter phone — DND on, brightness max, bookmark all 5 URLs from [[pitch/qr-codes]], open camera app once before walking on stage.*
- [ ] **Projector / big screen** — projection view (schematic + activity feed) legible from the back of the room; large type tested at distance.
  - *🧑 **Ready to run:** Open `https://fridson.lovable.app/projection?feed=real` on venue projector; stand at back of room; confirm schematic + feed text readable.*
- [ ] **Same network** — phone, presenter laptop, and projection machine on the **same Wi-Fi**; test the full scan→feed path on the *venue* network, not just hotel/home.
  - *🧑 **Ready to run:** Connect phone + laptop to venue Wi-Fi → scan hero QR → confirm report appears on projection within ~5s.*
- [ ] **Backup tab** — workspace open (shows persisted report if feed fails).
  - *🧑 **Ready to run:** Keep `https://fridson.lovable.app/workspace` in a background tab on the demo laptop.*

## B. Fallback recordings (🤝 collect from Tracks 1–3)
*Every live beat in [[pitch/script]] needs an armed recording. Queue in [[pitch/dry-run-checklist]]. Collect these before the dry-run.*

- [ ] **Full 60s flow** — screen capture of scan → pinpoint → report → route → bids → negotiate → book → approve (the whole Minute 1).
- [ ] **Scan → success** clip (Track 1) — in case the live scan fails.
- [ ] **Projection / activity feed** clip (Track 2) — scripted timeline if the live feed stalls.
- [ ] **Agent steps** clip (Track 3) — pre-fetched bids, a real sent RFQ email, pre-booked slot; the AI call clip if attempted.
- [ ] All cued in background tabs at 0:00; presenter knows the keystroke to switch to each.

## C. Day-2 check-in + Milestone-2 submission (🧑 human)

- [ ] **Sun ~09:00 — Day 2 check-in** on the [Z2D Dashboard](https://z2d-base.lovable.app/dashboard).
  - *🧑 **Ready to run:** Log in → complete Day 2 check-in form → confirm green status before build work continues.*
- [ ] **Harden the live path** (with Tracks 1–3) — no dead ends, fast load, fallbacks armed.
- [ ] **Lock the 3-min script** ([[pitch/script]]) — re-time at dry-run, adjust to hit exactly 3:00.
- [x] **Milestone 2 copy-paste fields drafted** — [[pitch/milestone-2-copy]] ✅
- [ ] **By Sun 15:00 — Milestone 2 submission** complete on the dashboard:
  - *🧑 **Ready to run:** Open [[pitch/milestone-2-copy]] → paste all fields → attach deck + demo recording → submit before 15:00.*
  - [ ] Project name **Fridson** + one-line description ("a suite of AI employees for property management").
  - [ ] Live app link (fridson.lovable.app) + repo link.
  - [ ] Pitch/deck attached; demo recording attached as backup.
  - [ ] Team roster: **Shuhia, Chris, Lennert** (per [[ACTIVE_PLAN]] — see §D).
- [ ] **Before Sun 16:00 — GATE: full-team dry-run** of the 3-min pitch; use [[pitch/dry-run-checklist]]; confirm acceptance criteria (exactly 3:00, each minute maps to source, every live beat has a tested fallback).
  - *🧑 **Ready to run:** Whole team on stage → run T-10 checklist → timed 3:00 run → optional failure drill from dry-run doc.*

## D. Decisions (resolved + open)

- [x] **Brand spelling — LOCKED: `Fridson`** ✅ *(decided 2026-06-28, Phase 4)*  
  Source doc ([[06-Wiki/decisions/2026-06-27-final-commitment]]) used **"Fritzson"**; repo, domain, and live app use **"Fridson"** (`fridson.lovable.app`, `github.com/westsoever/fridson`). **Decision: lock "Fridson"** — matches the URL judges will open; renaming domain/repo now is risk with no upside. Sweep deck + Milestone 2 submission for consistency (no "Fritzson").
- ~~**▶ Redeem Azure credits ($1,000)**~~ — **NOT NEEDED.** Agent runs on **Supabase Edge** (see [[ACTIVE_PLAN]] blockers — resolved). Azure does not unblock Track 3.
- [x] **Team roster — reconciled** ✅ *(documented 2026-06-28, Phase 4)*  
  | Source | Roster | Use for |
  |--------|--------|---------|
  | **[[ACTIVE_PLAN]]** (authoritative for dashboard) | Shuhia (admin), Chris, Lennert | **Milestone 2 submission** |
  | [[team.md]] (track ownership) | Chris, Slavi, Alex, Lennert + admin Shuhia | Build coordination only |
  | Prior logistics note | Slavi, Lennert, Chris, Alex | Superseded — was conflating track owners with dashboard members |

  **Submit Shuhia + Chris + Lennert** on the Z2D dashboard unless ACTIVE_PLAN is updated first. Slavi and Alex are track contributors (schematic/projection and agent backend) but are not listed as dashboard team members in ACTIVE_PLAN.

## E. Standing risks to watch (from [[ACTIVE_PLAN]])
- **Conference Wi-Fi** — rehearse on venue network; the recorded fallback is the insurance.
- **3-minute timing** — the live flow must be visible+explained in ~60s; rehearse the narration over the feed.
- **Fake-AI smell** — keep report + RFQ email real; label any pre-fetched data as such in rehearsal notes.
- **Scope discipline** — Minutes 2–3 are narrative/light-UI; don't let them pull build effort from the Minute-1 must-have.

---

## Pre-demo T-10-minute checklist (run on stage, off the clock)

Full version with fallback queue: [[pitch/dry-run-checklist]]

1. Projection view open + reset; legible from the back (`/projection?feed=real`).
2. Phone unlocked, camera open, on venue Wi-Fi, asset bookmarks ready.
3. 5 QR codes on the table; hero (`meeting-4f`) within reach.
4. Workspace backup tab open (`/workspace`).
5. Full-flow recording cued at 0:00; switch-keystroke confirmed.
6. Deck on the business-case slide for Minute 3; numbers memorized from [[pitch/business-case]].
