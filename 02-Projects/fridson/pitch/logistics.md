# Demo Logistics, Submission & Open Decisions

**Owner:** Track 4 (Pitch) · **Status:** Live checklist through Sun 16:00
**Anchors:** [[ACTIVE_PLAN]] Phase 7 · [[06-Wiki/decisions/2026-06-27-final-commitment]] · script in [[pitch/script]].
**Deadlines:** Milestone 2 submission **Sun 28 Jun 15:00** · Team dry-run before **16:00** · Live demo & judging **16:00**.

---

## A. Demo prop / hardware checklist (🧑 human)

- [ ] **Print 5 QR codes** — one per seeded asset, on the table as props:
  - [ ] `printer-3f` → `/r/printer-3f` (Printer · 3rd floor East)
  - [ ] `bathroom-2f` → `/r/bathroom-2f` (Bathroom · 2nd floor)
  - [ ] `meeting-4f` → `/r/meeting-4f` (Meeting room · 4th floor) — **hero asset for live scan**
  - [ ] `pump-basement` → `/r/pump-basement` (Pump room · Basement)
  - [ ] `kitchen-1f` → `/r/kitchen-1f` (Kitchen · Ground floor)
  - *Print large, high-contrast; tape to props or asset cards. Test each scans from ~30cm on the presenter phone.*
- [ ] **Presenter confirmed** — one person drives phone + narration (decide who; default the most rehearsed).
- [ ] **Phone ready** — unlocked, camera app primed, brightness up, notifications off, asset URLs bookmarked as scan-fallback.
- [ ] **Projector / big screen** — projection view (schematic + activity feed) legible from the back of the room; large type tested at distance.
- [ ] **Same network** — phone, presenter laptop, and projection machine on the **same Wi-Fi**; test the full scan→feed path on the *venue* network, not just hotel/home.
- [ ] **Backup tab** — admin/reports page open (shows persisted report if Slack/feed fails).

## B. Fallback recordings (🤝 collect from Tracks 1–3)
*Every live beat in [[pitch/script]] needs an armed recording. Collect these before the dry-run.*

- [ ] **Full 60s flow** — screen capture of scan → pinpoint → report → route → bids → negotiate → book → approve (the whole Minute 1).
- [ ] **Scan → success** clip (Track 1) — in case the live scan fails.
- [ ] **Projection / activity feed** clip (Track 2) — scripted timeline if the live feed stalls.
- [ ] **Agent steps** clip (Track 3) — pre-fetched bids, a real sent RFQ email, pre-booked slot; the AI call clip if attempted.
- [ ] All cued in background tabs at 0:00; presenter knows the keystroke to switch to each.

## C. Day-2 check-in + Milestone-2 submission (🧑 human)

- [ ] **Sun ~09:00 — Day 2 check-in** on the [Z2D Dashboard](https://z2d-base.lovable.app/dashboard).
- [ ] **Harden the live path** (with Tracks 1–3) — no dead ends, fast load, fallbacks armed.
- [ ] **Lock the 3-min script** ([[pitch/script]]) — re-time at dry-run, adjust to hit exactly 3:00.
- [ ] **By Sun 15:00 — Milestone 2 submission** complete on the dashboard:
  - [ ] Project name (resolve brand spelling first — see §D), one-line description ("a suite of AI employees for property management").
  - [ ] Live app link (fridson.lovable.app) + repo link.
  - [ ] Pitch/deck attached; demo recording attached as backup.
  - [ ] Team roster correct (see §D — Slavi, Lennert, Chris, Alex).
- [ ] **Before Sun 16:00 — GATE: full-team dry-run** of the 3-min pitch; confirm acceptance criteria (exactly 3:00, each minute maps to source, every live beat has a tested fallback).

## D. Open decisions to drive (🧑 human — blockers)

- [ ] **▶ Brand spelling — DECIDE FIRST (blocks deck/slides/submission).** Source doc says **"Fritzson"** ([[06-Wiki/decisions/2026-06-27-final-commitment]]); repo/domain/live app say **"Fridson"** (`fridson.lovable.app`, `github.com/westsoever/fridson`). **Recommendation: lock "Fridson"** — it matches the working domain, repo, and live demo URL judges will see; changing those now is risk with no upside. Once locked, sweep the deck + submission for consistency.
- [ ] **▶ Redeem Azure credits ($1,000)** — https://luma.link/aMPPeE5k4A — **unblocks Track 3 (Alex)**: hosts the agent service that runs route→bid→negotiate→book. Do this early Sun; the live agent beat depends on it.
- [ ] **Update team roster** — full team is **Slavi, Lennert, Chris, Alex**; [[02-Projects/fridson/team.md]] / ACTIVE_PLAN still list 3 (Shuhia, Chris, Lennert). Reconcile before submission so the dashboard roster is correct.

## E. Standing risks to watch (from [[ACTIVE_PLAN]])
- **Conference Wi-Fi** — rehearse on venue network; the recorded fallback is the insurance.
- **3-minute timing** — the live flow must be visible+explained in ~60s; rehearse the narration over the feed.
- **Fake-AI smell** — keep report + RFQ email real; label any pre-fetched data as such in rehearsal notes.
- **Scope discipline** — Minutes 2–3 are narrative/light-UI; don't let them pull build effort from the Minute-1 must-have.

---

## Pre-demo T-10-minute checklist (run on stage, off the clock)
1. Projection view open + reset; legible from the back.
2. Phone unlocked, camera open, on venue Wi-Fi, asset bookmarks ready.
3. 5 QR codes on the table; hero (`meeting-4f`) within reach.
4. Admin/reports backup tab open.
5. Full-flow recording cued at 0:00; switch-keystroke confirmed.
6. Deck on the business-case slide for Minute 3; numbers memorized from [[pitch/business-case]].
