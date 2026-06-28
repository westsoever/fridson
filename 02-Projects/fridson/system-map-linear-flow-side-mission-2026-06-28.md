# Side Mission Archive: System Map Linear Flow

**Completed:** 2026-06-28  
**Route:** `/graph` in `fridson-app`  
**Goal:** Rewire the System Map so each open ticket reads as a linear story — issue → asset → Fridson AI → report → provider — with no entry-method or infra hub nodes.

## What shipped

| Layer | Change |
|-------|--------|
| Topology | `src/lib/system-graph/build-graph.ts` — removed QR Entry, Supabase DB, Events Stream, PM/Research/Done; linear links only |
| AI node | Renamed **Triage AI** → **Fridson AI** (`pipeline/fridson-ai`) |
| Asset labels | `Bathroom - 2nd Floor` style via `formatAssetGraphLabel()` |
| Filters | `filter-graph.ts` — per-ticket path highlighting (no bleed through shared Fridson AI node) |
| Types/paint | Dropped `entry` node kind |

## Target chain (per open ticket)

```
No soap → Bathroom - 1st Floor → Fridson AI → Leak → Providers
 issue          asset              pipeline      ticket    (external only)
```

Inactive catalog nodes stay dimmed (~22% opacity). Fridson AI only links to assets/reports on active ticket paths.

## Verification

```
bun test src/lib/system-graph/  → 12 pass
bun run build                   → success
```

## Follow-up

- Commit + push `fridson-app/` to sync with Lovable (user action)
