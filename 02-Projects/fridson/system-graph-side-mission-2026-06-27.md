# Side Mission Archive: Live Data Flow Graph

**Completed:** 2026-06-27  
**Route:** `/graph` in `fridson-app`  
**Goal:** Obsidian-style force-directed map of all system datapoints, live-updated, with open-ticket highlighting and filters.

## What shipped

| Layer | Files |
|-------|-------|
| Topology model | `src/lib/system-graph/types.ts`, `build-graph.ts`, `filter-graph.ts` |
| Canvas | `src/components/system-graph/SystemGraph.tsx`, `node-paint.ts` |
| Filters + legend | `GraphFilters.tsx`, `GraphLegend.tsx` |
| Live data | `src/lib/system-graph.functions.ts`, `use-system-graph.ts` (4s poll) |
| Route | `src/routes/graph.tsx` + nav links on `/`, `/dashboard`, `/assets` |

**Dependency:** `react-force-graph-2d@1.29.1`

## Graph topology

- **Capture:** QR entry → assets → issue catalog (from `ISSUES`)
- **Tickets:** one node per open report (`status !== done`, no duplicate)
- **Pipeline:** Triage → PM → Research → Done
- **System:** Supabase DB hub, Events stream, Providers pool

Inactive nodes render at ~22% opacity; open-ticket paths get severity-colored rings.

## Filters (URL: `?filter=&value=`)

- **Show all** — full graph
- **Severity** — Low · Medium · High (dims non-matching paths)
- **Area** — Kitchen · Pump room · Meeting room · Bathroom · Printer

## Verification

```
bun test src/lib/system-graph/  → 9 pass
bun run build                   → success
```

## Node click navigation

- Report node → `/?selected={reportId}`
- Asset node → `/r/{assetId}`
