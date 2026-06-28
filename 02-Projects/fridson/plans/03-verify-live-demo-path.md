# Phase 3 — Verify Live Demo Path

**Goal:** End-to-end verification of capture → schematic → projection `?feed=real` → PM approve — matching ACTIVE_PLAN Phases 1–4 checklists.

**Prerequisites:** Phase 1 ([[01-deploy-gates]]) + Phase 2 ([[02-reconcile-agent-path]]) complete.

**Blocks:** Phase 7.

---

## Agent pickup instructions

> You are executing **Phase 3**. Read Phase 0. You may fix **critical demo bugs** only (routing, feed wiring, missing env reads). Do not build Minute 2 UI (Phase 5) or edit vault docs (Phase 6). Stage laptop setup is part of this phase.

---

## Sources consulted

Reference Phase 0, plus:

| Source | Checklist section |
|--------|-------------------|
| `02-Projects/fridson/ACTIVE_PLAN.md:95-155` | Phases 1–4 verification |
| `02-Projects/fridson/pitch/script.md:14-37` | Minute 1 beats + fallbacks |
| `fridson-app/src/routes/projection.tsx` | Stage projection page |
| `fridson-app/src/components/projection/use-feed.ts:13-18` | `?feed=real` |
| `fridson-app/src/routes/schematic.tsx` | Schematic markers |
| `fridson-app/src/routes/workspace.tsx` | PM approve |
| `fridson-app/src/routes/r.$assetId.tsx` | Capture flow |

---

## What to implement

This phase is **verification + stage setup**, not new features. Copy checklists from ACTIVE_PLAN and script.

### Stage laptop setup (copy from `pitch/script.md:14-18`)

1. Open **projection:** `https://fridson.lovable.app/projection?feed=real`
2. Click **Replay** to reset feed
3. Open **workspace** in background tab: `https://fridson.lovable.app/workspace`
4. Phone: same Wi-Fi, bookmarks for `/r/meeting-4f` (fallback if QR fails)
5. Confirm "Live feed" badge (green) not "Scripted demo"

**Copy feed resolution logic** from `use-feed.ts:13-18`:

- URL `?feed=real` overrides env
- Default is mock — **must** use query param on stage

---

## Verification checklist

### Phase 1 — Capture → Structured Report (ACTIVE_PLAN:103-108)

- [ ] All 5 routes load < 2s on phone/4G:
  - `/r/printer-3f`, `/r/bathroom-2f`, `/r/meeting-4f`, `/r/pump-basement`, `/r/kitchen-1f`
- [ ] Tap issue → success screen instant ("Sent to facility team" vs "Sent to contractor")
- [ ] Row appears in `/workspace` within 2s
- [ ] Two different issues show different routes (`inhouse` vs `external`)

**Commands:**

```bash
cd /Users/clyde/fridson/fridson-app && bun run build
curl -s -o /dev/null -w "%{http_code}" https://fridson.lovable.app/r/meeting-4f
# Expect 200
```

### Phase 2 — Schematic Pinpoint (ACTIVE_PLAN:118-121)

- [ ] Scan `meeting-4f` → marker on schematic within ~2s
- [ ] `/schematic` shows per-floor selector + open-report markers
- [ ] Schematic legible at projection distance (large type, test from 3m)

**Manual:** Submit report; watch `/projection` schematic panel for pulse at 4F coords.

**Coords source:** `fridson-app/public/floorplan.coords.json`, `components/schematic/coords.ts`

### Phase 3 — Agent loop (ACTIVE_PLAN:136-142)

Hero asset: `meeting-4f` → **"Projector broken"** (`pitch/script.md:10`)

- [ ] **Approve triggers agent** — PM clicks Approve on `awaiting_approval` ticket → `process-research` / resolution agent invoked async (202, no page hang)
- [ ] **Mock provider email** — agent selects seeded provider and sends RFQ via Resend mock path (`AGENT_LIVE_EMAIL=1` + team-controlled inbox); open message and verify report id, asset, issue, provider name
- [ ] Activity feed shows: providers selected → RFQs → bids → negotiate → slot booked
- [ ] Full sequence visible within ~60s
- [ ] PM Approve in workspace confirms booking
- [ ] Disapprove re-loops (optional smoke test)

**SQL verify:**

```sql
SELECT type, payload->>'provider' as provider, ts
FROM events WHERE report_id = '<hero_report_id>' ORDER BY ts;
```

### Phase 4 — Projection layer (ACTIVE_PLAN:151-154)

- [ ] One scan drives projected sequence **without extra clicks** on projection tab
- [ ] Step rail advances through: Report → Pinpoint → Providers → RFQ → Bids → Negotiate → Booked → Approved
- [ ] No raw JSON on screen — only `renderEvent()` output (`events.ts:70-144`)
- [ ] **Replay** button resets for second demo run

**Timing target:** visible flow ≤ ~60s (`pitch/script.md:0:30-1:00`)

### Approve flow (script beat)

Presenter taps **Approve** during Minute 1 (`script.md:30`):

- [ ] Workspace shows awaiting_approval report after triage
- [ ] Approve button works (`AIDecisionPanel` → `approveReport`) and **kicks off the agent**
- [ ] RFQ email received in mock/controlled inbox (not a live vendor address)
- [ ] If projection needs `pm.decision` event: verify it appears (Phase 2 decision)

### Fallback readiness (script:32-37)

- [ ] `/projection` without `?feed=real` runs mock timeline (backup)
- [ ] Bookmark `/r/meeting-4f` works as scan fallback
- [ ] Record whether live feed or mock was used in rehearsal notes

---

## Stage network checklist

- [ ] Phone + laptop on **same Wi-Fi** as venue (test on venue network if possible)
- [ ] Projection machine can reach `fridson.lovable.app`
- [ ] Supabase Realtime not blocked by firewall (if blocked, 2s poll fallback in `use-feed.ts:142` should still work)

---

## Anti-pattern guards

- ❌ Do not demo with default mock feed if claiming "live" — use `?feed=real`
- ❌ Do not skip hero asset test (`meeting-4f` / Projector broken)
- ❌ Do not assume triage completed — wait for `awaiting_approval` before approve
- ❌ Do not add new features — log gaps for Phase 5/7

---

## Documentation references

- [[../ACTIVE_PLAN|ACTIVE_PLAN]] Phases 1–4
- [[../pitch/script|pitch/script.md]]
- [[../pitch/logistics|pitch/logistics.md]] §A hardware
- `fridson-app/src/components/projection/events.ts` — STEP_SEQUENCE

---

## Handoff

Produce a **verification report** (pass/fail per checkbox) for Phase 7 dry-run. List any blockers with file:line references.
