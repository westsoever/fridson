# Property Dashboard & Insights — side mission (2026-06-27)

**Status:** Completed side mission (SIDEPLAN removed Jun 27)

## Goal

Read-only `/dashboard` page in `fridson-app/` — property KPIs, analytics charts, 10 most-recent reports, and a compact Insights panel. No schema changes; built only on existing `assets`, `reports`, `events`, `providers` data.

## Shipped (`fridson-app`)

- `src/lib/dashboard.functions.ts` — `getDashboardStats` server fn + `DashboardStats` type
- `src/routes/dashboard.tsx` — route, KPI cards, recent-10 feed
- `src/components/dashboard/Charts.tsx` — reports over time, by status, by asset type
- `src/components/dashboard/InsightPanel.tsx` — data points connected, daily failure rate, resolution/route stats
- Nav link in `index.tsx`; `routeTree.gen.ts` regenerated

## Commit

`459f217` on `fridson-app` `main` (pushed to Lovable)

## Scope guard

New files only + one additive nav link. Did not touch `reports.functions.ts`, `admin.tsx`, projection/schematic tracks.
