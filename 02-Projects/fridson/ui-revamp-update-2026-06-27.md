# Fridson UI revamp — update note (2026-06-27)

## Summary

Executed the design-system revamp plan against `fridson-app` (pushed to `main`). The operator home (`/`) is now a **decision-first triage workspace** aligned with research + `00-Inbox/design-system.md`, while preserving the durable AI pipeline (triage webhook → approve → research webhook).

## Shipped

### Operator workspace (`/`)

- **3-pane layout** refactored into workspace components under `src/components/workspace/`
- **Left:** Issue list with default **decision-first grouping** (unacknowledged urgent → duplicates → needs approval → in progress → done)
- **Center:** `WorkRecordPane` — evidence + editable brief fields; AI chat moved to **Discuss** tab (secondary, not primary)
- **Right:** `AIDecisionPanel` — urgency reasoning, acknowledge, approve/dispatch, research output, queue insights when nothing selected
- **Top:** `MissionControlStrip` KPI chips from `getQueueInsights()`
- **shadcn/ui** adopted across workspace (Button, Badge, Textarea, Tabs, Select, ScrollArea, Alert, Sonner toasts)
- **Design tokens** for urgency 1/2/3, AI accent, status categories in `src/styles.css`
- **Status labels** improved (`Awaiting approval`, `AI failed` vs bare `Failed`)

### Data layer

- Migration `20260627200000_triage_operations.sql`: `urgency`, `acknowledged_at`, `duplicate_of`, `safety_flag`, `photo_url`, `ai_reasoning`, `reporter_contact`, `report_audit_events`
- Server functions: `acknowledgeReport`, `mergeReports`, `getQueueInsights`, extended `submitReport` / `listReports`
- `process-triage` edge fn now writes `urgency` + `ai_reasoning` jsonb (keeps `ai_severity` for compat)

### Reporter flow

- `/r/$assetId` — 4-step GOV.UK-style flow: issue → safety gate → optional contact → submit
- `/report/$reportId/status` — public status page with short reference ID
- `getReport` server fn for status lookups

### Other

- `@tanstack/react-table` added (foundation for future dense inbox)
- Removed stale Slack copy from meta/assets page
- Nav link to `/dashboard` (analytics page from prior commit)

## Not done yet (follow-up)

- Phase 4: TanStack Table triage inbox + keyboard shortcuts (`j/k`, `cmd+k`)
- Phase 6: Full app shell nav (Mission Control, Triage, Issues, QR, Settings routes)
- Photo upload on reporter flow (storage wiring)
- Auth on operator routes
- Merge UI wired to `mergeReports` from duplicate clusters
- Run Supabase migration on deployed project

## Verify locally

```bash
cd fridson-app
bun run dev
# Operator: http://localhost:5173/
# Reporter: http://localhost:5173/r/<assetId>
# Status: http://localhost:5173/report/<id>/status
bun run build
```

## Sources

- Plan: chat session UI revamp plan v2
- Design system: `00-Inbox/design-system.md`
- Research: `00-Inbox/*-research.md`, `fridson-ai-issue-reporting-hmi-analysis.md`
