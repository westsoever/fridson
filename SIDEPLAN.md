# Side Mission: Live Data Flow Graph

**Goal:** Add a new `/graph` tab that renders an Obsidian-style force-directed map of every datapoint in the Fridson system, live-updated, with open tickets highlighted and inactive nodes greyed out.
**Scope:**
- In: new route + graph component, topology model (assets → reports → AI pipeline → DB), live polling/realtime, filters (Show all / Severity / Area), nav links from workspace + dashboard
- Out: global app shell refactor, 3D graph, IoT sensor nodes, duplicate-cluster graph analytics
**Done when:** `/graph` loads a force-directed graph showing the full data funnel; nodes without open tickets are grey; nodes on the path of an open ticket are highlighted by severity; filters re-render the graph; new reports appear within one refresh cycle without page reload.

---

## Up Next
- [ ] Commit + push `fridson-app` changes to sync with Lovable (user action)
- [ ] Run `/sideplan` → confirm delete `SIDEPLAN.md` now that archive exists

## In Progress
*(empty)*

## Done
- [x] Phase 1 — Graph topology model + `buildSystemGraph()` pure function (5 tests pass)
- [x] Phase 2 — Install `react-force-graph-2d` + base `SystemGraph` canvas component
- [x] Phase 3 — Live data wiring (reports + events) + active/inactive node styling
- [x] Phase 4 — Filter bar (Show all · Severity · Area)
- [x] Phase 5 — Route `/graph` + cross-page nav links
- [x] Phase 6 — Verification (9 tests pass, build success, anti-pattern grep clean)

## Blockers
- [ ] ❓ **Commit app changes** — `fridson-app/` has uncommitted work; needs explicit commit/push request to land on Lovable
- [ ] ❓ **Delete SIDEPLAN.md** — mission satisfies "Done when"; archive at `02-Projects/fridson/system-graph-side-mission-2026-06-27.md` is ready

## Session Log
| Date | Summary |
|------|---------|
| 2026-06-27 | Side mission created. Phase 0 doc discovery complete. |
| 2026-06-27 | All 6 phases executed in `/do` run. `/graph` route live, 9 tests pass, build green. Archived to `02-Projects/fridson/system-graph-side-mission-2026-06-27.md`. |
| 2026-06-27 | `/sidewrap`: mission verified complete. Remaining: commit `fridson-app`, delete `SIDEPLAN.md`. |

---

**Mission status: COMPLETE** — run `/sideplan` and confirm deletion when ready.
