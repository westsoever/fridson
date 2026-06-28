# Phase 4 — Pitch Logistics

**Goal:** Complete human-action queue for brand, QR prints, hardware, dry-run scheduling, Milestone 2 submission, and fallback recordings.

**Prerequisites:** Phase 0 read. Can run **in parallel** with Phases 1–3.

**Blocks:** Phase 7 (dry-run needs hardware + fallbacks).

---

## Agent pickup instructions

> You are executing **Phase 4**. This is primarily **human logistics** — draft checklists, generate QR assets, update pitch docs. Do **not** change `fridson-app/` code. Coordinate with team for physical tasks (print, present, submit).

---

## Sources consulted

| Source | Content |
|--------|---------|
| `02-Projects/fridson/pitch/logistics.md` | Full logistics checklist |
| `02-Projects/fridson/pitch/script.md` | Setup, fallbacks, timing |
| `02-Projects/fridson/ACTIVE_PLAN.md:57-66,186-198` | Human-action queue, Phase 7 |
| `02-Projects/fridson/pitch/business-case.md` | Minute 3 numbers |

---

## What to implement

Copy tasks from `pitch/logistics.md` — do not invent new deadlines.

### A. Brand spelling (DECIDE FIRST — blocks deck/submission)

**Copy from `logistics.md:47`:**

- Source doc: "Fritzson" · Repo/domain: **"Fridson"**
- **Recommendation: lock "Fridson"** — matches live URL judges will see
- Sweep deck + Milestone 2 submission for consistency

**Remove stale Azure blocker** from team comms — agent runs on Supabase Edge (`ACTIVE_PLAN.md:258`).

### B. QR codes (5 assets)

**Copy from `logistics.md:11-17`:**

| Asset | URL |
|-------|-----|
| `printer-3f` | `https://fridson.lovable.app/r/printer-3f` |
| `bathroom-2f` | `https://fridson.lovable.app/r/bathroom-2f` |
| `meeting-4f` | `https://fridson.lovable.app/r/meeting-4f` (**hero**) |
| `pump-basement` | `https://fridson.lovable.app/r/pump-basement` |
| `kitchen-1f` | `https://fridson.lovable.app/r/kitchen-1f` |

- Print large, high-contrast
- Test scan from ~30cm on presenter phone

### C. Hardware (logistics.md §A)

- [ ] Presenter confirmed (one person: phone + narration)
- [ ] Phone: unlocked, camera ready, notifications off, asset URL bookmarks
- [ ] Projector / big screen: projection legible from back of room
- [ ] Same Wi-Fi: phone, laptop, projection machine
- [ ] Backup tab: `/workspace` open

### D. Fallback recordings (logistics.md §B)

Arm before dry-run — each live beat in `script.md:32-37`:

- [ ] **Full 60s flow** — scan → pinpoint → report → route → bids → negotiate → book → approve
- [ ] Scan → success clip
- [ ] Projection / activity feed clip (mock timeline)
- [ ] Agent steps clip (pre-fetched bids, pre-booked slot)
- [ ] All cued in background tabs at 0:00; switch keystroke confirmed

### E. Z2D submissions

**Copy from `logistics.md:33-43` + ACTIVE_PLAN schedule:**

| When | Action |
|------|--------|
| Sun ~09:00 | **Day 2 check-in** — [Z2D Dashboard](https://z2d-base.lovable.app/dashboard) |
| Sun **15:00** | **Milestone 2** — project name, one-liner, live app link, repo, deck, demo recording |
| Before **16:00** | **GATE: full-team dry-run** — exactly 3:00 |

**Milestone 2 fields:**

- Project name: Fridson (once locked)
- One-liner: *"Fridson is a suite of AI employees for property management"*
- Live app: https://fridson.lovable.app
- Repo: https://github.com/westsoever/fridson-app
- Team roster: reconcile Slavi, Lennert, Chris, Alex vs ACTIVE_PLAN 3-person list

### F. Pre-demo T-10 checklist (logistics.md:59-65)

Run on stage, off the clock:

1. `/projection?feed=real` open + reset
2. Phone on venue Wi-Fi
3. 5 QR codes on table; hero within reach
4. `/workspace` backup tab
5. Full-flow recording cued
6. Business-case slide ready; numbers memorized

---

## Documentation references

- [[../pitch/logistics|pitch/logistics.md]]
- [[../pitch/script|pitch/script.md]]
- [[../pitch/business-case|pitch/business-case.md]]
- [[../ACTIVE_PLAN|ACTIVE_PLAN]] Phase 7, Human-Action Queue

---

## Verification checklist

- [ ] Brand spelling decided and documented (one line in team chat or logistics.md checkbox)
- [ ] 5 QR codes printed and scanned successfully
- [ ] Presenter + hardware assigned
- [ ] Venue Wi-Fi tested (or fallback recording confirmed)
- [ ] Day 2 check-in complete
- [ ] Milestone 2 submitted by 15:00
- [ ] Fallback recordings exist and are cued
- [ ] Dry-run scheduled before 16:00

---

## Anti-pattern guards

- ❌ Do not redeem Azure credits for agent hosting — not needed
- ❌ Do not block build team on logistics — run in parallel
- ❌ Do not submit with "Fritzson" if brand locked to Fridson
- ❌ Do not skip fallback recordings — conference Wi-Fi is a standing risk

---

## Agent scope note

If no human is available, agent can:

- Generate QR code PNGs/links document
- Update logistics.md checkboxes
- Draft Milestone 2 copy-paste text

Cannot: print QR codes, present on stage, submit to dashboard without human credentials.
