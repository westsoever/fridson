# Phase 6 — Doc Reconciliation

**Goal:** Update vault docs (`ACTIVE_PLAN.md`, `ROADMAP.md`) so checkboxes and blockers match verified code reality. Remove stale Azure references.

**Prerequisites:** Phase 0 read. Best after Phase 1–3 report their status.

**Parallel with:** Phases 1–4. **No app code changes.**

---

## Agent pickup instructions

> You are executing **Phase 6**. Edit vault files in `02-Projects/fridson/` only. Do **not** touch `fridson-app/`. Use Phase 0 verified facts + Phase 1–3 handoff reports. One status-log line per session max.

---

## Sources consulted

| Source | Why |
|--------|-----|
| [[00-documentation-discovery|Phase 0]] | Verified build state |
| `02-Projects/fridson/ACTIVE_PLAN.md` | Phases, blockers, status log |
| `02-Projects/fridson/ROADMAP.md` | Item statuses |
| `02-Projects/fridson/pitch/logistics.md` | Stale Azure mention §D |
| Phase 1–3 completion notes | What's actually deployed |

---

## What to implement

### 1. ACTIVE_PLAN.md checkboxes

Update to match post-Phase-1/2/3 reality:

| Section | Likely updates |
|---------|----------------|
| Phase 1 (95-101) | Workspace on Lovable live after migration |
| Phase 2 (113-116) | Schematic pushed; pinpoint verify checkbox |
| Phase 3 (127-134) | Provider directory seeded; agent steps per chosen path |
| Phase 4 (146-149) | Projection built; wire real feed checkbox |
| Blockers (248-266) | Push/migrate/deploy checked; agent path decided |
| Human queue (57-66) | Remove or strike Azure redeem; note Fridson spelling rec |

**Copy status format** from existing log entries (`ACTIVE_PLAN.md:270-291`).

### 2. ROADMAP.md statuses

Update legend items (#1–#11) per verified state:

| Item | Current code reality |
|------|---------------------|
| #1 Capture | ✅ built, verify on live |
| #2 Schematic | 🔨 local pushed after Phase 1 |
| #3 Directory | ✅ 55 providers in migration |
| #4–#7 Agent loop | 🔨 resolution agent built; deploy pending |
| #8 Projection | ✅ built; real feed needs Phase 1+2 |
| #9 Context UI | ⏭️ Phase 5 optional |
| #10 Business case | 🤝 pitch docs exist |
| #11 Demo props | 🧑 Phase 4 |

Update **Last updated** date to 2026-06-28.

### 3. Remove stale Azure references

**Files to sweep:**

| File | Stale content | Action |
|------|---------------|--------|
| `ACTIVE_PLAN.md:63,239` | Azure credits blocker | Mark resolved / not needed |
| `ROADMAP.md:50` | "Azure/email API" dependency | Change to Supabase Edge + optional Resend |
| `pitch/logistics.md:48` | Azure unblocks Track 3 | Strike or update |

**Fact:** `ACTIVE_PLAN.md:258` already notes Azure NOT needed.

### 4. Team roster

Reconcile `pitch/logistics.md:49` (Slavi, Lennert, Chris, Alex) vs `ACTIVE_PLAN.md:227-232` (Shuhia, Chris, Lennert) — pick authoritative list or note both.

### 5. Add plans index link

Ensure `ACTIVE_PLAN.md` references `plans/README.md` in Team & Resources or Session Protocol.

---

## Documentation references

- [[00-documentation-discovery|Phase 0 verified facts]]
- [[../plans/README|plans/README.md]]
- `02-Projects/fridson/team-plans/INTERFACES.md` — authoritative DB shapes

---

## Verification checklist

- [ ] No checkbox claims "not built" for shipped features (projection, schematic, agent)
- [ ] No checkbox claims "done" for unverified live deploy
- [ ] Azure marked resolved/not required everywhere
- [ ] Blockers section reflects Phase 1–2 outcomes
- [ ] ROADMAP `Last updated` is current
- [ ] Status log has reconciliation entry (date + summary)

```bash
# Grep for stale Azure
rg -i "azure" 02-Projects/fridson/ --glob "*.md"
# Each hit should be struck, archived, or marked not needed
```

---

## Anti-pattern guards

- ❌ Do not edit `fridson-app/` in this phase
- ❌ Do not mark deploy gates complete without Phase 1 confirmation
- ❌ Do not delete historical status log entries — append only
- ❌ Do not re-debate canonical definition — link to Final Commitment

---

## Handoff

Docs should match what Phase 7 dry-run actually tests. If Phase 3 failed items, leave checkboxes open with note.
