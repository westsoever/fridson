# Plan: System Map — Linear Ticket Flow

**Status:** Implemented (`fridson-app` commit `fd3caeb`)  
**Scope:** `fridson-app/` route `/graph` (sidebar: "System Map")  
**Goal:** Simplify the graph to a single ticket path — no entry-method nodes, no Supabase hub — with **Fridson AI** as the intake endpoint before tickets branch to providers.

---

## Target topology

```
No Soap  →  Bathroom - 2nd Floor  →  Fridson AI  →  Leak (report)  →  Provider
 issue          asset                  pipeline         ticket          system
```

**Remove from graph:**
- `QR Entry` (`entry/qr`) — entry *method* is not a node
- `Supabase DB` (`system/db`) and `Events Stream` (`system/events`) — no infra hub
- `PM Review`, `Research Agent`, `Done` — post-AI workflow not shown on map

**Rename:** `Triage AI` → **Fridson AI**

**Restructure links:** Fridson AI must not fan in from every issue/report. One linear active path per open ticket.

---

## Phase 0: Documentation Discovery

### Sources consulted

| Source | What it defines |
|--------|-----------------|
| `fridson-app/src/lib/system-graph/build-graph.ts` | All nodes, links, activation |
| `fridson-app/src/lib/system-graph/types.ts` | `GraphNodeKind`, link shape |
| `fridson-app/src/lib/system-graph/filter-graph.ts` | Severity/area highlighting via ticket path walk |
| `fridson-app/src/lib/issues.ts:6-37` | Issue catalog labels |
| `fridson-app/src/lib/system-graph/build-graph.test.ts` | Topology assertions |
| `02-Projects/fridson/system-graph-side-mission-2026-06-27.md` | Original design (partially stale) |

### Allowed APIs (do not invent)

- **Graph builder:** `buildSystemGraph(assets, reports)` → `{ nodes, links }`
- **Node kinds:** `"asset" | "issue" | "report" | "pipeline" | "system"`
- **Stable IDs:** `asset/{id}`, `issue/{assetId}/{slug}`, `report/{id}`, `pipeline/fridson-ai`, `system/providers`
- **Link shape:** `{ source, target, kind, active }`
- **Activation:** `hasOpenTicket` on nodes; `active` on links
- **Canvas:** `react-force-graph-2d` in `SystemGraph.tsx` — no API changes needed

### Anti-patterns to avoid

- Do not add new node kinds or DB fields — topology is code-only in `build-graph.ts`
- Do not link every catalog issue to Fridson AI — only paths with open tickets
- Do not reintroduce infra hub nodes (Supabase DB, Events Stream)

---

## Phase 1: Remove infra & entry nodes ✅

**File:** `src/lib/system-graph/build-graph.ts`

- Removed `ENTRY_NODE_ID` / QR Entry node
- Removed `Supabase DB` and `Events Stream` system nodes
- Kept `Providers` (`system/providers`)
- Removed `"entry"` from `GraphNodeKind` in `types.ts`
- Removed entry styling branch in `node-paint.ts`

---

## Phase 2: Rename Triage AI → Fridson AI ✅

- Single pipeline node: `FRIDSON_AI_NODE_ID = "pipeline/fridson-ai"`, label `"Fridson AI"`
- Removed PM Review / Research Agent / Done pipeline stages

---

## Phase 3: Rewire links to linear ticket flow ✅

### Link rules (shipped)

| Kind | Source → Target | `active` when |
|------|-----------------|---------------|
| `issue-asset` | issue → asset | issue has open ticket for that asset+label |
| `asset-fridson` | asset → `pipeline/fridson-ai` | open report on that asset |
| `fridson-report` | `pipeline/fridson-ai` → report | report is open |
| `report-providers` | report → `system/providers` | `route === "external"` |

Catalog-only `issue → asset` links exist for every issue/asset pair with `active: false` when no ticket. Inactive issues do **not** link to Fridson AI.

### Asset labels

`formatAssetGraphLabel(name, zone)` → e.g. `"Bathroom - 1st Floor"`, `"Meeting room - 2nd Floor"`.

---

## Phase 4: Fix filters ✅

**File:** `src/lib/system-graph/filter-graph.ts`

Replaced forward-walk from `ENTRY_NODE_ID` with `pathForReport()` — walks backward from each matching report through Fridson AI, asset, and issue nodes (matching report label).

---

## Phase 5: Verification ✅

```bash
cd fridson-app
bun test src/lib/system-graph/   # 12 pass
bun run build                    # success
```

### Manual QA checklist (`/graph`)

1. **No open tickets:** All nodes dimmed; no QR Entry, Supabase DB, or Events Stream; catalog issue→asset edges visible at low opacity.
2. **One open bathroom ticket:** Path lights up: issue → Bathroom - … → Fridson AI → report → Provider (provider only if external).
3. **Filters:** Severity and area filters dim unrelated subtrees.
4. **Click:** Report node → `/?selected={id}`; asset node → `/r/{assetId}`.

---

## Files changed

| File | Change |
|------|--------|
| `src/lib/system-graph/build-graph.ts` | Topology rewrite |
| `src/lib/system-graph/filter-graph.ts` | Ticket-path highlighting |
| `src/lib/system-graph/build-graph.test.ts` | Linear chain assertions |
| `src/lib/system-graph/types.ts` | Dropped `"entry"` kind |
| `src/components/system-graph/node-paint.ts` | Dropped entry styling |

No changes to `SystemGraph.tsx`, `GraphFilters.tsx`, or Supabase fetch layer.
