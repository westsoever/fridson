# Phase 2 — Reconcile Agent Path

**Goal:** Decide and implement **one canonical agent path** for the demo so a single scan triggers a coherent flow: triage → projection events → PM approve.

**Prerequisites:** Phase 1 complete ([[01-deploy-gates|01-deploy-gates]]) — migrations and functions deployed.

**Blocks:** Phase 3, 7.

---

## Agent pickup instructions

> You are executing **Phase 2**. Read Phase 0 first. You **own** `fridson-app/src/lib/reports.functions.ts`, `agent-invoke.server.ts`, and optionally edge function wiring. Do **not** change migrations (Phase 1) or projection UI (Phase 3/5). Document the decision in a comment at the call site.

---

## Sources consulted

Reference [[00-documentation-discovery#allowed-apis-list-with-file-citations|Phase 0 Allowed APIs]], plus:

| Source | What it defines |
|--------|-----------------|
| `fridson-app/src/lib/reports.functions.ts:128-180` | `submitReport` — dual trigger today |
| `fridson-app/src/lib/reports.functions.ts:197-226` | `approveReport` — research webhook |
| `fridson-app/src/lib/agent-invoke.server.ts:23-40` | Resolution agent POST |
| `fridson-app/supabase/migrations/20260627180100_report_agent_webhooks.sql` | pg_net triggers |
| `fridson-app/HANDOFF.md:8-21` | Webhook flow diagram |
| `fridson-app/supabase/functions/agent/README.md:73-86` | Events emitted for projection |
| `02-Projects/fridson/ACTIVE_PLAN.md:255,264` | Recommends webhook-only OR pick one |
| `02-Projects/fridson/team-plans/INTERFACES.md:42-57` | Event feed contract |

---

## Problem statement (verified)

On every `submitReport`:

1. **DB webhook** fires `process-triage` (INSERT trigger) — updates `ai_summary`, `status → awaiting_approval`
2. **`invokeResolutionAgent(reportId)`** fires POST to `/functions/v1/agent` — emits `providers.selected` → … → `slot.booked` into `events`

These serve **different purposes**:

| Path | Updates report row | Emits `events` for projection |
|------|-------------------|-------------------------------|
| Webhook (`process-triage` / `process-research`) | ✅ | ❌ |
| Resolution agent (`agent`) | Best-effort status | ✅ |

The **3-min pitch** needs projection events (`pitch/script.md:0:45-1:00`). The **workspace UI** needs triage fields (`AIDecisionPanel`).

---

## Options (pick ONE for demo)

### Option A — Hybrid (recommended for pitch)

**Keep both**, but ensure they don't conflict:

- Webhook: triage + research (workspace UI, Slack if configured)
- Resolution agent: projection feed events only

**Implementation:** No removal; verify both run without double-booking. Optionally add idempotency guard in agent if duplicate runs observed.

**Copy pattern:** Current code at `reports.functions.ts:173-177` — leave `invokeResolutionAgent` in place; comment documents intent.

### Option B — Resolution agent only (projection-first)

**Remove/disable** INSERT webhook trigger for demo; agent handles full loop.

**Copy to change:**

```typescript
// reports.functions.ts:173-177 — REMOVE invokeResolutionAgent block
// AND disable trigger (migration or manual):
// DROP TRIGGER on_report_created ON public.reports;
```

**Risk:** Workspace triage fields (`ai_summary`) won't populate unless agent writes them.

### Option C — Webhook only (workspace-first)

**Remove** `invokeResolutionAgent` call; rely on mock projection feed.

**Copy to change** (`reports.functions.ts:176-177`):

```typescript
// DELETE these lines:
// const { invokeResolutionAgent } = await import("./agent-invoke.server");
// await invokeResolutionAgent(reportId);
```

**Stage setup:** Use `/projection` without `?feed=real` (mock timeline). Script fallback at `pitch/script.md:35`.

**Risk:** Minute 1 "live feed" beat is scripted, not real.

---

## What to implement (recommended: Option A with verification)

### 1. Document the decision

Add a brief comment block above the invoke call in `reports.functions.ts:173`:

```typescript
// Demo path (Phase 2): process-triage webhook → workspace AI fields;
// invokeResolutionAgent → events table → /projection?feed=real
```

### 2. Verify approve flow alignment

**Workspace approve** (`approveReport` → `process-research`) finds contractors with pricing.

**Pitch approve** (`script.md:0:45-1:00`) expects projection `pm.decision` event.

If using resolution agent for projection, PM approve on stage should **also** call agent decision API OR workspace approve must emit `pm.decision` event.

**Check:** Does `approveReport` emit `pm.decision` to `events`? Currently **no** — only resolution agent's `/agent/decision` does.

**Copy pattern for projection approve** (if needed — from `agent/README.md:101-109`):

```typescript
// Optional: after approveReport succeeds, call agent decision endpoint
await fetch(`${SUPABASE_URL}/functions/v1/agent/decision`, {
  method: "POST",
  headers: { "Content-Type": "application/json", apikey: key, Authorization: `Bearer ${key}` },
  body: JSON.stringify({ report_id: reportId, decision: "approve" }),
});
```

Only add if E2E test in Phase 3 shows projection stalls at "Booked" without `pm.decision`.

### 3. Do NOT invent new APIs

Use only documented endpoints from Phase 0 Allowed APIs list.

---

## Documentation references

- `fridson-app/supabase/functions/agent/README.md` — HTTP API, events
- `fridson-app/HANDOFF.md` — webhook flow
- [[../team-plans/INTERFACES|INTERFACES §4–§5]]
- [[../RESOLUTION-AGENT|Resolution Agent spec]]

---

## Verification checklist

### Resolution agent offline tests

```bash
cd /Users/clyde/fridson/fridson-app/supabase/functions/agent
deno task test    # 10 tests, offline
deno task demo    # prints full event sequence
```

Expected: all tests pass.

### Single trigger check

1. Submit one test report via `/r/meeting-4f`
2. Query `events` table (Supabase dashboard or SQL):

```sql
SELECT type, ts FROM events WHERE report_id = '<id>' ORDER BY ts;
```

Expected sequence (resolution agent path):

- `report.created`, `location.pinpointed` (DB trigger — Track 1)
- `providers.selected`, `rfq.sent`, `bid.received`, `negotiation.round`, `slot.booked` (agent)

3. Check report row status progression (webhook path):

- `awaiting_ai` → `awaiting_approval` within ~10s

### No duplicate agent runs

```bash
# Grep for duplicate invoke paths
rg "invokeResolutionAgent|process-triage" fridson-app/src/
```

Expected: one invoke site in `submitReport`; triage via DB only (not also in `retryReport` except explicit retry).

### Projection real feed

Open `/projection?feed=real`, submit report, confirm events appear within ~30s.

---

## Anti-pattern guards

- ❌ Do not leave both paths firing without verifying projection + workspace both work
- ❌ Do not add a third agent trigger
- ❌ Do not change INTERFACES event type strings — projection parser expects exact types (`events.ts:10-18`)
- ❌ Do not block `submitReport` on agent completion
- ❌ Do not enable autonomous spend — booking stays hold until approve

---

## Handoff

Document chosen option (A/B/C) in commit message or Phase 2 completion note. Phase 3 runs full E2E with that path.
