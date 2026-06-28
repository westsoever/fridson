# Phase 5 — Minute 2 Context UI (Optional)

**Goal:** Build mock stakeholder lens UI (insurer / energy / compliance) on a ticket page — per `pitch/ecosystem.md` and script Minute 2.

**Prerequisites:** Phase 0 read. Ideally Phase 3 confirms report/ticket shape. **Optional** — skip if time runs short (Minute 2 deliverable on slides alone).

**Parallel with:** Phases 1–3 if UI-only; avoid conflicting with Phase 2 files.

---

## Agent pickup instructions

> You are executing **Phase 5** (optional). Read Phase 0 + `pitch/ecosystem.md`. Copy UI patterns from existing workspace components. Do **not** modify `reports.functions.ts`, edge functions, or migrations. Add a route or panel only.

---

## Sources consulted

| Source | Content |
|--------|---------|
| `02-Projects/fridson/pitch/ecosystem.md` | 3 stakeholder lenses, triage-shift line |
| `02-Projects/fridson/pitch/script.md:41-52` | Minute 2 beats |
| `02-Projects/fridson/ACTIVE_PLAN.md:157-168` | Phase 5 scope + anti-patterns |
| `fridson-app/src/components/workspace/WorkRecordPane.tsx` | Ticket detail layout |
| `fridson-app/src/components/workspace/AIDecisionPanel.tsx` | Panel + badge patterns |
| `fridson-app/src/components/ui/tabs.tsx` | Lens toggle pattern |

---

## What to implement

**Copy framing from `ecosystem.md:38-47`** — one ticket, multiple lenses on the same event. No real integrations.

### 1. Stakeholder lens toggle

Add a **Tabs** or **ToggleGroup** on ticket detail showing:

| Lens | Shows (mock copy from ecosystem.md) |
|------|-------------------------------------|
| **Property manager** | asset · location · issue · route · cost · approval |
| **Insurer** | detection time · response time · resolution proof |
| **Energy / utility** | asset type · failure mode · repair history |
| **Compliance** | full timestamped chain + sign-off |

**Example ticket:** bathroom leak (`bathroom-2f`) — `ecosystem.md:24`

**Copy UI pattern from workspace:**

- Layout: `workspace.tsx` three-pane structure
- Cards: `components/ui/card.tsx`
- Badges: `components/ui/badge.tsx` (see `AIDecisionPanel.tsx:17-18` urgency badges)

### 2. Route options

Pick one (minimal scope):

- **A)** Add lens tabs to `WorkRecordPane.tsx` when report selected
- **B)** New route `/ticket/$reportId/context` linked from workspace

Prefer **A** if it fits without large refactor.

### 3. Data source

Read existing report fields from `listReports` shape (`reports.functions.ts:41-43`):

- `created_at`, `asset_label`, `zone`, `issue_label`, `status`, `approved_at`, `contractors`
- Derive mock insurer/energy/compliance copy in component — **no new DB columns**

**Copy timestamp formatting** from projection: `events.ts:54-58` `formatDate()`.

### 4. Triage-shift visual (script 1:45-2:00)

Simple split card:

- Before: "PM orchestrates everything"
- After: "PM approves"

Static content — no API.

---

## Documentation references

- [[../pitch/ecosystem|pitch/ecosystem.md]]
- [[../pitch/script|pitch/script.md]] Minute 2
- [[../05-Knowledge/stakeholder-painpoint-value-map|stakeholder map]]
- `fridson-app/src/components/workspace/` — patterns to copy

---

## Verification checklist

### Build

```bash
cd /Users/clyde/fridson/fridson-app
bun run build
```

### Against script Minute 2 (`script.md:44-48`)

- [ ] Ticket page shows ≥2 stakeholder lenses on same event
- [ ] Can cycle insurer / energy / compliance views
- [ ] Triage-shift line fits ≤20s when narrated (`ecosystem.md:51-55`)
- [ ] Fallback: static slide still works if toggle breaks (script:51)

### Manual

1. Open `/workspace`, select a report with `done` or `awaiting_approval` status
2. Toggle each lens — content updates, same report ID
3. No login required

---

## Anti-pattern guards

- ❌ Do not build real insurer/energy API integrations
- ❌ Do not add migrations or new tables for mock lenses
- ❌ Do not pull effort from Phase 1–3 critical path
- ❌ Do not invent unsourced stats in lens copy — use ecosystem.md examples

---

## Skip criteria

Skip this phase if:

- Phase 3 verification not complete by Sun 14:00
- Team has static ecosystem slide ready (`script.md:51` fallback)

Minute 2 is **narrative-first** — slides alone satisfy the pitch.
