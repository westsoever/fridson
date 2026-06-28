# Phase 0 — Documentation Discovery

**Goal:** Establish allowed APIs, anti-patterns, and verified build state so every later phase is self-contained.

**Prerequisites:** None — run this first (or read this file before any implementation phase).

**Deadline context:** Z2D demo Sun 28 Jun 16:00.

---

## Agent pickup instructions

> You are executing **Phase 0** (discovery only). Read the sources below. Do **not** change app code or vault docs unless explicitly asked. Output: confirm the Allowed APIs list and Current Build State match reality; flag any drift to the orchestrator.

---

## Sources consulted

| Source | What was read |
|--------|---------------|
| `02-Projects/fridson/ACTIVE_PLAN.md` | Phases, blockers, status log |
| `02-Projects/fridson/ROADMAP.md` | Build sequence, dependencies |
| `02-Projects/fridson/team-plans/INTERFACES.md` | Report shape, events contract, Track 1 notes |
| `fridson-app/HANDOFF.md` | Webhook agent flow, deploy checklist |
| `fridson-app/supabase/functions/agent/README.md` | Resolution agent HTTP API, events |
| `fridson-app/src/lib/reports.functions.ts` | `submitReport`, `approveReport`, `retryReport` |
| `fridson-app/src/lib/agent-invoke.server.ts` | `invokeResolutionAgent` seam |
| `fridson-app/src/routes/projection.tsx` | Projection page, `?feed=real` |
| `fridson-app/src/components/projection/use-feed.ts` | Realtime + poll on `events` |
| `fridson-app/src/components/projection/events.ts` | Event types, `renderEvent` |
| `fridson-app/supabase/config.toml` | `verify_jwt` for edge functions |
| `fridson-app/supabase/migrations/` | 22 SQL files (Track 1 + webhooks + triage ops) |
| `fridson-app/supabase/functions/` | `agent`, `process-triage`, `process-research`, `_shared` |

---

## Allowed APIs list (with file citations)

### Report lifecycle (app server functions)

| API | Location | Purpose |
|-----|----------|---------|
| `submitReport({ assetId, issueLabel, ... })` | `fridson-app/src/lib/reports.functions.ts:128-180` | INSERT report; fires webhook + resolution agent |
| `approveReport({ reportId, brief_summary?, brief_instructions? })` | `reports.functions.ts:197-226` | UPDATE status → `approved`; fires research webhook |
| `retryReport({ reportId, phase: "triage" \| "research" })` | `reports.functions.ts:228-253` | Re-trigger triage or research |
| `listReports()`, `getReport()`, `acknowledgeReport()`, `mergeReports()` | `reports.functions.ts` | Workspace/admin reads and ops |

### Resolution agent invoke (app → edge)

| API | Location | Purpose |
|-----|----------|---------|
| `invokeResolutionAgent(reportId)` | `fridson-app/src/lib/agent-invoke.server.ts:23-40` | POST `{ report_id }` to `/functions/v1/agent`; never throws |

### Resolution agent HTTP (edge function)

| Method | Route | Location |
|--------|-------|----------|
| `GET` | `/agent` | `supabase/functions/agent/README.md:56-63` |
| `POST` | `/agent` `{ report_id }` or `{ report:{…} }` | async 202 |
| `POST` | `/agent?wait=1` | sync run (tests only) |
| `POST` | `/agent/decision` `{ report_id, decision }` | PM gate |
| `GET` | `/agent/run?report_id=…` | cached run state |

### Webhook agents (DB → edge via pg_net)

| Trigger | Function | Location |
|---------|----------|----------|
| AFTER INSERT on `reports` | `process-triage` | `migrations/20260627180100_report_agent_webhooks.sql:14-37` |
| AFTER UPDATE status→`approved` | `process-research` | same file:39-64 |

### Projection feed

| API | Location | Purpose |
|-----|----------|---------|
| `resolveFeedSource(searchParam?)` | `use-feed.ts:13-18` | `mock` default; `?feed=real` or `VITE_PROJECTION_FEED=real` |
| `useProjectionFeed({ source, assetId, reportId })` | `use-feed.ts:35-158` | Realtime INSERT + 2s poll on `events` |
| `renderEvent(event)` | `events.ts:70-144` | Human-readable step cards |

### Data shapes (INTERFACES §1 — authoritative in DB)

| Field | Actual values | Source |
|-------|---------------|--------|
| `route` | `inhouse` \| `external` | `INTERFACES.md:81` |
| `status` | `awaiting_ai` \| `awaiting_approval` \| `approved` \| `researching` \| `done` \| `failed` | `INTERFACES.md:82` |
| `events.type` | `report.created`, `location.pinpointed`, `providers.selected`, … | `events.ts:10-18`, migration `20260627190300` |

### Edge function config

```toml
# fridson-app/supabase/config.toml:6-15
[functions.agent]           verify_jwt = false
[functions.process-triage]  verify_jwt = false
[functions.process-research] verify_jwt = false
```

Project ref: `yyidatcqbvsbntdavmww` (`config.toml:1`)

---

## Anti-patterns (do NOT do)

| Anti-pattern | Why |
|--------------|-----|
| Invent API methods not in tables above | Causes deploy/runtime failures |
| Use `route: "in-house"` or `status: "open"` | DB uses `inhouse` / `awaiting_ai` (INTERFACES §Track 1 notes) |
| Block scan success on agent completion | Both agent paths are async by design |
| Rebuild Capture (`/r/{asset}`) | Works; extend only |
| Add login, payments, CAD import, real insurer integrations | Out of demo scope |
| Force-push `fridson-app` main | Lovable-connected; see `AGENTS.md` |
| Assume Azure is required | Agent runs on Supabase Edge (ACTIVE_PLAN blockers, resolved) |
| Show raw JSON on projection stage | Use `renderEvent()` only |
| Commit vault notes to app repo | Two separate git repos |

---

## Current build state (verified facts — 2026-06-28)

### App repo git

```
Local main:  e4234ec (schematic floor selector + report markers)
             ↑ 3 commits ahead of fd3caeb
Origin main: 7d85c50 (Lovable "Synced recent changes")
             ↑ 3 commits ahead of fd3caeb
Status: DIVERGED — merge origin/main before push
```

Local-only commits: `1702293`, `de7d3fc`, `e4234ec` (schematic enhancements).

### Routes (built in code)

| Route | Status | Notes |
|-------|--------|-------|
| `/r/{assetId}` | ✅ Live | Scan→tap capture |
| `/workspace` | ✅ Shipped `72af388` | PM triage + approve |
| `/projection` | ✅ Built | Mock default; `?feed=real` for live |
| `/schematic` | ✅ Local only | Per-floor selector + markers (`e4234ec`) |
| `/dashboard`, `/graph` | ✅ `fd3caeb` on origin | Side missions |
| `/` | Redirects to `/dashboard` | `index.tsx:4-6` |

### Data spine (migrations in repo, may not be live)

- `assets.location` + `floorplan.svg` + 55 `providers` rows
- `events` table + auto-emit `report.created` + `location.pinpointed` on INSERT
- `report_agent_webhooks` pg_net triggers
- `20260627200000_triage_operations.sql` — urgency, acknowledge, audit events

**22 migration files** total in `supabase/migrations/`. Live DB state unknown until `db push`.

### Two agent systems (both active in code)

1. **Resolution agent** (`supabase/functions/agent/`) — emits INTERFACES §4 events for projection
2. **Webhook agents** (`process-triage`, `process-research`) — triage/research on report row; **do not** emit projection events

`submitReport` currently calls **both** webhook (via INSERT trigger) and `invokeResolutionAgent` (`reports.functions.ts:173-177`).

### Projection

- Mock feed works offline (`mock-emitter.ts`)
- Real feed needs: migrations applied, `events` populated by resolution agent, Realtime enabled
- PM approve for pitch script: `/workspace` `AIDecisionPanel` → `approveReport` (not on `/projection`)

### Not built

- Stakeholder lens UI (Minute 2) — no `stakeholder`/`lens` code in app
- Real RFQ email (optional; stub works)
- CAD import, voice calls, sensors, payments

### Pitch docs (vault)

- `02-Projects/fridson/pitch/script.md` — locked 3-min script
- `pitch/logistics.md`, `pitch/ecosystem.md`, `pitch/business-case.md`

---

## Verification checklist (Phase 0)

Discovery is complete when an agent can answer yes/no to each:

- [ ] `git -C fridson-app status` shows divergence state
- [ ] `ls fridson-app/supabase/functions/` lists `agent`, `process-triage`, `process-research`
- [ ] `rg invokeResolutionAgent fridson-app/src/` finds `reports.functions.ts` + `agent-invoke.server.ts`
- [ ] `rg process-triage fridson-app/supabase/migrations/` finds webhook trigger
- [ ] `/projection?feed=real` logic exists in `use-feed.ts:74-155`

No build/test required for Phase 0.

---

## Confidence & known gaps

| Item | Confidence | Gap |
|------|------------|-----|
| Code structure | High | Read from workspace files |
| Live Supabase state | **Unknown** | Migrations/functions may not be applied — Phase 1 verifies |
| Lovable sync commits on origin | Medium | Contents of `7d85c50` not diffed; merge may conflict with schematic |
| Real email / Firecrawl | Low | Secrets not verified in this session |

---

## Documentation references

- [[../ACTIVE_PLAN|ACTIVE_PLAN]]
- [[../ROADMAP|ROADMAP]]
- [[../team-plans/INTERFACES|INTERFACES]]
- [[../RESOLUTION-AGENT|Resolution Agent spec]]
- `fridson-app/HANDOFF.md`
- `fridson-app/supabase/functions/agent/README.md`
