# Plan: System Map Topology Rewrite

> **App target:** `fridson-app/` route `/graph` ("System Map" tab)  
> **Prior work:** `02-Projects/fridson/system-graph-side-mission-2026-06-27.md`  
> **Goal:** Replace hub topology (QR Entry fan-out, Triage AI star, Supabase DB sink) with per-ticket linear chains ending at Fridson AI then routing outcomes.

Each phase is self-contained for a fresh chat session. Run `git fetch` in vault + `fridson-app` before editing.

---

## Product intent (from request)

| Change | Meaning |
|--------|---------|
| Remove **Supabase DB** as entry/hub | DB is not a graph node users traverse; data still comes from Supabase in `system-graph.functions.ts` |
| No **capture-method** nodes | Remove `QR Entry` (`entry/qr`); no nodes for "how it got entered" |
| Rename **Triage AI** → **Fridson AI** | Label change on pipeline triage node |
| **Linear chains**, not hub | Fridson AI must not link to every issue; only the active ticket path is linked |

**Canonical example chain (external bathroom leak):**

```
No Soap → Bathroom - 2nd Floor → Fridson AI → Leak → Provider
```

**Implementation interpretation (no `ai_routed_label` in schema today):**

- **Link direction** follows narrative: `issue` → `asset` → `pipeline/triage` (Fridson AI) → terminus.
- For an **external** report with `issue_label: "Leak"`: `Leak` → `Bathroom - 2nd Floor` → `Fridson AI` → `Providers`.
- The user's `No Soap` → … → `Leak` sequence implies AI **reclassification** (soap report routed as leak). That needs a future DB field; **Phase 2** implements direct external routing (`Fridson AI` → `Providers`) unless/until `ai_routed_label` (or similar) exists.
- For **inhouse** reports: `issue` → `asset` → `Fridson AI` → `PM Review` → `Research Agent` → `Done`.

Inactive catalog nodes (issues/assets with no open ticket) remain on the canvas at low opacity but **have no links** (no structural fan-out).

---

## Phase 0: Documentation Discovery ✅

### Allowed APIs (verified — do not invent)

| Layer | Source | What exists |
|-------|--------|-------------|
| Graph builder | `src/lib/system-graph/build-graph.ts` | `buildSystemGraph`, `ENTRY_NODE_ID`, `PIPELINE_NODE_IDS`, `SYSTEM_NODE_IDS`, `buildLinks`, `applyActivation` |
| Types | `src/lib/system-graph/types.ts` | `GraphNodeKind` includes `"entry"`; link shape `{ source, target, kind, active }` |
| Filters | `src/lib/system-graph/filter-graph.ts` | `filterGraph`, `expandForward`, `ENTRY_NODE_ID` injection on asset highlight |
| Tests | `src/lib/system-graph/build-graph.test.ts`, `filter-graph.test.ts` | 9 tests; assert `entry/qr`, hub links |
| Issue catalog | `src/lib/issues.ts` | `ISSUES[asset.type]` drives issue node labels/routes |
| Data fetch | `src/lib/system-graph.functions.ts` | `getSystemGraphData` — Supabase `assets` + `reports` (not a graph node) |
| Canvas | `src/components/system-graph/SystemGraph.tsx` | Force layout only; no topology |
| Node paint | `src/components/system-graph/node-paint.ts` | `case "entry"` radius/fill |
| Page | `src/routes/graph.tsx` | Title "System Map" |

### Current topology (hub — to remove)

Copy reference: `build-graph.ts:117-126` (QR Entry node), `254-320` (link fan-out).

```
entry/qr ──► every asset ──► every issue ──► pipeline/triage (Triage AI)
open report ──► pipeline/triage (bypasses asset/issue in links)
open report (external) ──► system/providers
pipeline stages ──► system/db ──► system/events
```

### Anti-patterns to avoid

- Do **not** add new graph node kinds for "QR", "entry method", or "Supabase DB" as user-facing flow steps
- Do **not** keep `pushLink(issueId, PIPELINE_NODE_IDS.triage)` for **every** catalog issue — only for issues with open reports
- Do **not** keep `pushLink(ENTRY_NODE_ID, assetId)` or the `entry/qr` node
- Do **not** keep `pipeline-db` / `db-events` fan-in unless product explicitly re-adds infra nodes later
- Do **not** rename `pipeline/triage` ID unless you update all tests and `PIPELINE_NODE_IDS` consumers — **label-only rename is sufficient**
- Do **not** edit `system-graph.functions.ts` for topology (data layer stays the same)

### Node ID scheme (keep stable)

| Kind | ID pattern | Label source |
|------|------------|--------------|
| Asset | `asset/{assetId}` | `assets.name` (e.g. "Bathroom - 2nd Floor" from DB) |
| Issue | `issue/{assetId}/{slug}` | `ISSUES` catalog + `slugifyLabel` |
| Report | `report/{reportId}` | `report.issue_label` |
| Pipeline | `pipeline/triage` etc. | `PIPELINE_LABELS` map |
| System | `system/providers` | `"Providers"` (keep); remove `system/db`, `system/events` nodes |

---

## Phase 1: Remove entry + infra hub nodes

**What to implement:** Delete capture-method and DB hub nodes; strip links that depend on them.

### Copy from (pattern to delete, not extend)

1. **QR Entry node** — `build-graph.ts:117-126`
2. **Supabase DB + Events nodes** — `build-graph.ts:163-176`
3. **Entry + DB links** — `build-graph.ts:257`, `307-319`
4. **DB activation** — `build-graph.ts:241-242`

### Tasks

1. In `buildStaticNodes`, remove the `ENTRY_NODE_ID` block and `system/db` + `system/events` nodes.
2. Remove `export const ENTRY_NODE_ID` (or leave exported empty — prefer **delete** and fix imports).
3. In `buildLinks`, remove all `entry-asset`, `pipeline-db`, and `db-events` links.
4. In `applyActivation`, remove `SYSTEM_NODE_IDS.db` and `SYSTEM_NODE_IDS.events` updates.
5. In `SYSTEM_NODE_IDS`, remove `db` and `events` keys (grep `SYSTEM_NODE_IDS` across app).
6. In `filter-graph.ts`, delete `ENTRY_NODE_ID` import and lines 37-38 (entry re-injection).
7. In `types.ts`, remove `"entry"` from `GraphNodeKind` if no longer used.
8. In `node-paint.ts`, remove `case "entry"` branches in `nodeRadius` and `activeNodeFill`.

### Verification checklist

```bash
cd fridson-app
rg "entry/qr|ENTRY_NODE_ID|Supabase DB|Events Stream|system/db|pipeline-db" src/
# Expect: no matches (or only archive/docs outside src)
bun test src/lib/system-graph/
```

### Anti-pattern guards

- Supabase remains the **data source** in `system-graph.functions.ts` — only remove **graph nodes** labeled "Supabase DB"
- Do not remove `system/providers` — it is the external terminus

---

## Phase 2: Linear per-ticket chains + Fridson AI rename

**What to implement:** Rewire `buildLinks` so each open report creates one forward path; rename triage label.

### Copy from (keep these helpers)

- `issueNodeId`, `assetNodeId`, `reportNodeId` — `build-graph.ts:45-55`
- `openReportsForIssue`, `isPipelineStageActive` — activation logic stays
- Pipeline chain loop pattern — `build-graph.ts:293-305` (keep PM → Research → Done **after** Fridson AI)

### Target link algorithm (replace `buildLinks` body)

For each **open report** `r`:

1. `issueNodeId(r.asset_id, r.issue_label)` → `assetNodeId(r.asset_id)` — kind `issue-asset`, `active: true`
2. `assetNodeId(r.asset_id)` → `PIPELINE_NODE_IDS.triage` — kind `asset-fridson`, `active: true`
3. **Optional report anchor:** `reportNodeId(r.id)` → `issueNodeId(...)` — kind `report-issue`, `active: true` (keeps report node on chain for click → `/?selected=`)

**If `r.route === "external"`:**

4. `PIPELINE_NODE_IDS.triage` → `SYSTEM_NODE_IDS.providers` — kind `fridson-providers`, `active: true`

**If `r.route === "inhouse"`:**

4. Existing pipeline chain: triage → pm → research → done (only when respective stage active)

**Do not add:**

- Links from inactive issues to Fridson AI
- Links from Fridson AI to inactive issues/assets
- Direct `report` → `pipeline/triage` (remove `report-triage` kind)
- Direct `report` → `providers` (remove `report-providers`; path goes through Fridson AI)

**For assets/issues with no open report:** emit **zero** links involving those nodes.

**Rename:**

```ts
// build-graph.ts PIPELINE_LABELS
triage: "Fridson AI",
```

### Fixture for new test (add to `build-graph.test.ts`)

```ts
const bathroom2f: GraphAsset = {
  id: "bathroom-2f",
  name: "Bathroom - 2nd Floor",
  type: "bathroom",
  zone: "2F",
  location: null,
};

const leakReport: GraphReport = {
  id: "report-bathroom-leak",
  asset_id: "bathroom-2f",
  issue_label: "Leak",
  route: "external",
  status: "triaging",
  duplicate_of: null,
};

// Assert active links (order matters for chain):
// issue/bathroom-2f/leak → asset/bathroom-2f → pipeline/triage → system/providers
```

Add second fixture for inhouse `No soap` → assert chain ends at `pipeline/pm` when status is `awaiting_approval`, not at Providers.

### Update existing tests

| Test | Change |
|------|--------|
| `uses stable deterministic node IDs` | Remove `entry/qr` expectation |
| `links kitchen asset to four issue nodes` | Expect **0** `asset-issue` links when no open reports (or remove test if links only exist with tickets) |
| `activates kitchen asset, issue, and triage...` | Assert `issue-asset` + `asset-fridson` + `issue-triage` removed; assert new kinds |
| `filter-graph.test.ts` | Severity/area filters seed from report/issue/asset — re-run after topology change; may need `expandForward` to also walk **backward** from seeds if chain is issue → asset → AI |

### Filter graph adjustment (likely required)

`expandForward` only walks link direction. Seeds today include `asset` and `issue` nodes. With links `issue → asset → Fridson AI`:

- **Area filter** seeds asset/issue nodes — forward walk reaches Fridson AI ✓
- **Severity filter** seeds report + matching issue + asset — forward from issue reaches asset, Fridson AI, Providers ✓
- If seeds start at **asset only**, forward walk may **not** reach **issue** (upstream). Options (pick one in implementation):
  - **A (recommended):** Build **bidirectional** adjacency for highlight expansion only
  - **B:** Add reverse links for filter-only (avoid — duplicates topology)
  - **C:** Change seed logic to always include issue node when asset is seeded

Document choice in commit; prefer **A** in `filter-graph.ts` `buildForwardAdjacency`.

### Verification checklist

```bash
cd fridson-app
bun test src/lib/system-graph/
bun run build
```

Manual on `/graph`:

- [ ] No "QR Entry" node
- [ ] No "Supabase DB" or "Events Stream" nodes
- [ ] Node labeled "Fridson AI" (not "Triage AI")
- [ ] Fridson AI has edges only along active ticket paths (no star to all bathroom issues)
- [ ] External ticket: path reaches "Providers" after Fridson AI
- [ ] Inhouse ticket: path continues PM → Research → Done after Fridson AI

### Anti-pattern guards

- Do not link every inactive catalog issue for layout "completeness"
- Do not reintroduce `report-triage` shortcut edges

---

## Phase 3: Canvas polish (optional, if layout still looks hub-like)

**What to implement:** Tune force layout so chains read left-to-right.

### Copy from

- `SystemGraph.tsx` — `configureForces` / `link.distance` / `charge` settings (read file; adjust distances per link kind if exposed)

### Tasks

1. Increase link distance on `fridson-providers` and pipeline-chain links slightly so terminus nodes separate from AI.
2. Optionally weaken global charge so disconnected inactive nodes cluster by `group` without pulling active chain apart.

### Verification

- Visual check on `/graph` with 2+ simultaneous open tickets — two distinct chains, Fridson AI not a dense star.

---

## Phase 4: Verification + docs

### Tasks

1. Run full graph test suite + build (same as Phase 2).
2. Grep anti-patterns:

```bash
rg "Triage AI|QR Entry|Supabase DB|entry/qr|issue-triage|report-triage|pipeline-db" fridson-app/src/
```

3. Update `02-Projects/fridson/system-graph-side-mission-2026-06-27.md` topology section OR add changelog note at top pointing to this plan.

### Success criteria

| Criterion | Proof |
|-----------|-------|
| No entry-method nodes | `build-graph` has no `kind: "entry"` |
| No DB hub nodes | No `system/db` / `system/events` in node list |
| Fridson AI label | `PIPELINE_LABELS.triage === "Fridson AI"` |
| Linear external chain | Test: Leak → Bathroom 2F → Fridson AI → Providers |
| Linear inhouse chain | Test: issue → asset → Fridson AI → pm (when status matches) |
| Filters still work | `filter-graph.test.ts` passes |
| 9+ tests green | `bun test src/lib/system-graph/` |

---

## Delegation matrix

| Phase | Parallelizable tasks |
|-------|-------------------|
| 1 | `build-graph.ts` node removal ∥ `filter-graph.ts` entry cleanup ∥ `node-paint.ts` + `types.ts` |
| 2 | `buildLinks` rewrite ∥ test fixture updates ∥ `filter-graph` bidirectional adjacency |
| 3 | Force tuning only after Phase 2 visual check |
| 4 | Docs ∥ grep audit |

## Files touched (summary)

| File | Phases |
|------|--------|
| `src/lib/system-graph/build-graph.ts` | 1, 2 |
| `src/lib/system-graph/filter-graph.ts` | 1, 2 |
| `src/lib/system-graph/build-graph.test.ts` | 2 |
| `src/lib/system-graph/filter-graph.test.ts` | 2 |
| `src/lib/system-graph/types.ts` | 1 |
| `src/components/system-graph/node-paint.ts` | 1 |
| `src/components/system-graph/SystemGraph.tsx` | 3 (optional) |
| `02-Projects/fridson/system-graph-side-mission-2026-06-27.md` | 4 |

**No changes expected:** `graph.tsx`, `GraphLegend.tsx`, `system-graph.functions.ts`, `use-system-graph.ts`

---

## Open product questions (resolve before or during Phase 2)

1. **AI reclassification node** — Is `No Soap` → `Fridson AI` → `Leak` required now, or is `Fridson AI` → `Providers` enough until schema has routed label?
2. **Report nodes** — Keep as ticket anchor on chain, or hide report nodes and use issue node clicks only?
3. **PM / Research / Done** — Still shown for inhouse after Fridson AI, or collapse to Fridson AI as sole AI step?

Default implementation if unanswered: (1) direct to Providers for external, (2) keep report node at chain start, (3) keep full inhouse pipeline after Fridson AI.
