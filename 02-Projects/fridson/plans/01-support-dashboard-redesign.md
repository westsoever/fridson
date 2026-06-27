# Plan: Support Dashboard UI Redesign (HostoGo-style)

> **Side mission:** `SIDEPLAN.md` at vault root  
> **App target:** `fridson-app/`  
> **Reference:** HostoGo Tech Support Dashboard screenshot (2026-06-28)  
> **Priority 1:** Recent Tickets activity feed — vertically stacked ticket cards

Each phase is self-contained for a fresh chat session. Use **parallel subagents** within a phase where tasks are independent (see Delegation Matrix at bottom).

---

## Phase 0: Documentation Discovery ✅

### Allowed APIs (verified — do not invent)

| Layer | Source | What exists |
|-------|--------|-------------|
| **Routing** | `src/router.tsx`, `src/routes/*.tsx` | TanStack Start file routes; no shared layout route yet |
| **Reports (tickets)** | `src/lib/reports.functions.ts` | `listReports`, `getReport`, `getQueueInsights`, `acknowledgeReport`, `approveReport`, … |
| **Dashboard stats** | `src/lib/dashboard.functions.ts` | `getDashboardStats()` — counts, 14-day volume, resolution rate |
| **Status tokens** | `src/lib/tokens/status.ts` | `STATUS_META`, `statusMeta()` — canonical chip classes |
| **Urgency tokens** | `src/lib/tokens/urgency.ts` | `urgencyBadgeClass`, `urgencyDotClass` |
| **Activity feed** | `src/components/projection/ActivityFeed.tsx` | Vertical scroll list pattern (projection events, not tickets) |
| **Charts** | `src/components/dashboard/Charts.tsx` + `ui/chart.tsx` | Recharts via `ChartContainer` — line, pie, bar |
| **Sidebar (unused)** | `src/components/ui/sidebar.tsx` | Full shadcn `SidebarProvider`, `SidebarMenuButton`, badges |
| **Breadcrumb (unused)** | `src/components/ui/breadcrumb.tsx` | Compound breadcrumb API — zero route usage |
| **Card primitive** | `src/components/ui/card.tsx` | Standard shadcn Card |
| **DB model** | `src/integrations/supabase/types.ts` | `reports` table (no `tickets` table); `events` for agent activity |

### Anti-patterns to avoid

- Do **not** create a `tickets` table — map UI "tickets" to `reports`
- Do **not** duplicate `STATUS_META` — import from `@/lib/tokens/status`
- Do **not** use Chart.js — only Recharts + `ChartContainer`
- Do **not** assume sidebar is wired — it exists but is **unimported** in routes
- Do **not** build SLA/assignment/auth backends in UI phases — shell + copy only until schema exists

### Domain mapping (screenshot → Fridson)

| Screenshot | Fridson equivalent |
|------------|-------------------|
| All tickets / Open / Overdue | `reports` filtered by `status`, `urgency`, `acknowledged_at` |
| Recent tickets feed | `listReports()` sorted by `created_at` desc |
| Ticket Reply Time chart | Derive from `report_messages` timestamps or mock until wired |
| Ticket Priority gauge | Map `ai_severity` + `route` (inhouse/external) |
| Avg tickets created/solved | `getDashboardStats().reportsByDay` + done counts |
| Sidebar "Support" active | New `/support` route (Support Overview) |
| "+ Add New" | Link to `/r/$assetId` or future create-ticket modal |

### Sidebar tabs → implementation tier

| Tab | Phase | Tier |
|-----|-------|------|
| **Dashboard** (Support Overview) | 3 | Full widgets + live data |
| **Recent tickets feed** | 2 | **P1 — build first** |
| Ticket assignment | 4 | Settings shell + feature copy |
| Ticket topics | 4 | Settings shell (extend `issues.ts` catalog UI) |
| SLA management | 4 | Settings shell (no schema yet) |
| Custom ticket statuses | 4 | Settings shell (extend `status.ts` concept) |
| Joint editing | 4 | Shell (collab = `report_messages` chat exists) |
| Email integration | 4 | Shell (Resend in agent edge fn exists) |
| Authorization management | 4 | Shell (auth middleware exists, not wired) |
| Reporting and statistics | 3 | Reuse `/dashboard` charts in new shell |

---

## Phase 1: App Shell Layout

**What to implement:** Shared operator layout with left sidebar, top breadcrumb bar, and content outlet — matching screenshot structure.

### Copy from (do not reinvent)

1. **Sidebar scaffold** — `src/components/ui/sidebar.tsx:49-147` (`SidebarProvider`, menu button patterns)
2. **Top nav link styling** — `src/routes/dashboard.tsx:77-97` (uppercase tracked links — adapt for sidebar)
3. **Route + loader pattern** — `src/routes/dashboard.tsx:22-36`

### Tasks

1. Create `src/components/layout/AppShell.tsx`
   - Wrap children in `SidebarProvider`
   - Left column: logo "Fridson", user placeholder, primary nav items with Lucide icons
   - Badge on "Activity" nav item (count from `getQueueInsights().urgentUnacknowledged`)
   - Secondary nav group: Support (active state), Library, Invoices, Automation placeholders
   - Bottom: "Need Help?" button
2. Create `src/components/layout/PageHeader.tsx`
   - Breadcrumbs via `ui/breadcrumb.tsx`: e.g. `Support / Support Overview`
   - Right-aligned `Button` with `Plus` icon: "+ Add New"
3. Create `src/config/navigation.ts` — single source for nav items, paths, icons, badges
4. Add layout route or wrap existing operator routes:
   - Option A (recommended): `src/routes/_operator.tsx` layout route with `<Outlet />`
   - Option B: wrap each page individually (more duplication)

### New routes (stubs OK in Phase 1)

| Path | Label |
|------|-------|
| `/support` | Support Overview (default landing) |
| `/support/assignment` | Ticket assignment |
| `/support/topics` | Ticket topics |
| `/support/sla` | SLA management |
| `/support/statuses` | Custom ticket statuses |
| `/support/collaboration` | Joint editing |
| `/support/email` | Email integration |
| `/support/authorization` | Authorization management |
| `/support/reports` | Reporting and statistics |

Keep existing `/` (issue workspace) accessible — either migrate under shell or link from sidebar as "Triage".

### Verification checklist

- [ ] `bun run dev` — `/support` renders sidebar + header without layout shift
- [ ] Sidebar collapses on mobile (sheet behavior from shadcn sidebar)
- [ ] Active nav item highlights correctly per route
- [ ] `grep -r "SidebarProvider" src/routes` returns layout usage
- [ ] No duplicate top-nav headers on shell-wrapped pages

### Anti-pattern guards

- Do not import sidebar internals piecemeal — use exported `Sidebar`, `SidebarMenu`, `SidebarMenuButton`
- Do not hardcode nav in every route — use `navigation.ts`

---

## Phase 2: Recent Tickets Feed (Priority 1)

**What to implement:** The screenshot's bottom-right "Recent tickets" panel — vertically stacked cards with date, title, snippet, status pill, left color bar, hover arrow.

### Copy from

1. **Card list structure** — `src/routes/dashboard.tsx:130-158` (recent reports list)
2. **List row with badge** — `src/components/workspace/IssueRow.tsx:13-54`
3. **Status pills** — `src/lib/tokens/status.ts:11-65` (`statusMeta(report.status).chip`)
4. **Feed container** — `src/components/projection/ActivityFeed.tsx:73-79` (vertical `flex-col gap-3`)
5. **Empty state** — `src/components/workspace/EmptyState.tsx:10-23`

### Component contract

```
src/components/support/RecentTicketsFeed.tsx
src/components/support/TicketCard.tsx
```

**`TicketCard` props:**

```ts
type TicketCardProps = {
  id: string
  createdAt: string       // formatted "Feb 08, 2024"
  title: string           // issue_label or brief_summary
  snippet: string         // ai_summary truncated
  status: ReportStatus
  urgency?: 1 | 2 | 3
  isOverdue?: boolean     // computed: urgency=3 && !acknowledged_at (proxy until SLA)
  href: string            // /?reportId=… or /support/tickets/$id
  isHovered?: boolean     // optional controlled hover for Storybook
}
```

**Visual spec (from screenshot):**

- Card: white bg, rounded-xl, subtle shadow, full width in feed column
- Left edge: 3px vertical color bar — red (overdue), blue (open), green (completed), orange (pending)
- Header row: date (muted, small) + status pill (right)
- Title: semibold, single line truncate
- Snippet: 2-line clamp, muted
- Hover: elevated shadow + top-right arrow icon (`ArrowUpRight`)
- Section header: "Recent tickets" + ghost "View all" button

**Data wiring:**

- `listReports()` → sort by `created_at` desc → take 8
- Map `status` → pill label via `statusMeta()`
- Map `urgency === 3 && !acknowledged_at` → "Overdue" override pill (red)
- Poll every 8s (match dashboard pattern)

### Verification checklist

- [ ] Feed renders 8 stacked cards with correct status colors
- [ ] Hover state shows arrow affordance
- [ ] Click navigates to ticket detail (workspace or detail route)
- [ ] Empty state when no reports
- [ ] Uses `@/lib/tokens/status` — no local STATUS_META duplicate
- [ ] Component Storybook or visual snapshot optional

### Anti-pattern guards

- Do not reuse `StepCard` (projection events) — tickets have different fields
- Do not fetch in `TicketCard` — parent feed owns the query

---

## Phase 3: Support Overview Dashboard Page

**What to implement:** Full `/support` page grid matching screenshot — KPI row, charts, Recent Tickets feed.

### Layout grid (12-col)

```
Row 1: [ KPI ] [ KPI ] [ KPI ] [ KPI ]     — 4 equal cards
Row 2: [ Ticket Reply Time chart (7 col) ] [ Priority gauge (5 col) ]
Row 3: [ Avg tickets bar chart (7 col) ]   [ RecentTicketsFeed (5 col) ]
```

### Copy from

1. **KPI cards** — `src/routes/dashboard.tsx:62-68, 107-119`
2. **Charts** — `src/components/dashboard/Charts.tsx:47-126`
3. **Insight panel tiles** — `src/components/dashboard/InsightPanel.tsx:57-105`
4. **Loader + polling** — `src/routes/dashboard.tsx:10-20`

### KPI mapping

| Screenshot KPI | Data source |
|----------------|-------------|
| All tickets | `stats.reports.total` |
| Client replies | Count `report_messages` where role=user (new query or mock) |
| Staff replies | Count assistant/system messages (mock Phase 3) |
| Tickets without reply | Open reports with no `report_messages` (mock Phase 3) |

### Chart widgets

1. **Ticket Reply Time** — Line chart; start with `stats.reportsByDay` from dashboard stats; refine later
2. **Ticket Priority** — Donut/pie chart; segment by `ai_severity` or `route`
3. **Average Tickets Created** — Bar chart; solved vs created per day from `getDashboardStats()`

Extract reusable widgets to `src/components/support/widgets/`:

- `SupportKpiRow.tsx`
- `TicketReplyTimeChart.tsx`
- `TicketPriorityChart.tsx`
- `AvgTicketsChart.tsx`

### Page assembly

`src/routes/support/index.tsx` — compose shell + widgets + `RecentTicketsFeed`

### Verification checklist

- [ ] Page matches screenshot grid proportions at 1280px+ viewport
- [ ] KPI numbers update on 8s poll
- [ ] Charts render with empty-state fallbacks
- [ ] Recent Tickets feed live in bottom-right slot
- [ ] `bun run build` passes

---

## Phase 4: Sidebar Feature Section Shells

**What to implement:** Placeholder pages for each sidebar tab with title, description (from user requirements), and "Coming soon" or minimal config UI.

### Page template (copy once)

`src/components/support/FeatureShell.tsx`:

- PageHeader with breadcrumb `Support / {Feature name}`
- Hero card with feature description (user-provided copy below)
- Optional: settings form skeleton (disabled inputs)

### Feature copy (use verbatim in UI)

| Route | Title | Description |
|-------|-------|-------------|
| `/support/assignment` | Ticket assignment | Automatically assign tickets to agents and groups based on keywords, requests, or characteristics. |
| `/support/topics` | Ticket topics | Create ticket topics with important information such as categories, software used, plugin version, error message, feature requests, etc. |
| `/support/sla` | SLA management | Set deadlines for ticket response and resolution times depending on business hours or categories. |
| `/support/statuses` | Custom ticket statuses | Create custom status messages that adapt to your unique workflow. This way you can easily see the processing status of a ticket. |
| `/support/collaboration` | Joint editing | Collaborate on tickets with other teams and keep track of progress. |
| `/support/email` | Email integration | Convert issues into trackable tickets in your support ticket system for better management and resolution. |
| `/support/authorization` | Authorization management | Give account managers specific access and action permissions based on their roles and responsibilities. |
| `/support/reports` | Reporting and statistics | Easily access data and reports to get tailored insights relevant to your daily operations. |

**Dashboard tab note:** The user listed "Dashboard — Responds quickly and consistently to frequently update the interface and therefore property supervisor." Interpret as: Support Overview (`/support`) uses aggressive polling (8s) + optimistic UI — already specified in Phase 3.

### Verification checklist

- [ ] All 8 routes render inside AppShell
- [ ] Sidebar active state correct on each route
- [ ] Breadcrumbs reflect current section

---

## Phase 5: Live Data, Interaction & Polish

**What to implement:** Wire remaining real data, navigation flows, design polish.

### Tasks

1. **"+ Add New"** — navigate to asset picker or `/assets` with create intent
2. **"View all"** on Recent Tickets — link to `/` workspace or future `/support/tickets`
3. **Ticket card click** — deep-link to `/?reportId={id}` (existing search param in workspace)
4. **Activity badge** — wire sidebar count from `getQueueInsights()`
5. **Align colors** with screenshot palette in `styles.css` if needed:
   - Overdue: red-500 bar / red-100 pill
   - Open: blue
   - Completed: emerald
   - Pending: amber/orange
6. **Remove duplicate headers** from legacy routes wrapped by shell
7. **Consolidate** dashboard: redirect `/dashboard` → `/support/reports` or embed charts

### Verification checklist

- [ ] End-to-end: listReports → TicketCard → workspace selection works
- [ ] Polling refreshes feed without scroll jump (preserve scroll position)
- [ ] Mobile: feed stacks full width below charts
- [ ] Lighthouse: no regressions on LCP for shell

---

## Phase 6: Final Verification

1. **Build:** `cd fridson-app && bun run build`
2. **Grep anti-patterns:**
   - `rg "STATUS_META" src/routes` — should not duplicate status.ts
   - `rg "chart.js|ChartJS" src` — should be empty
   - `rg "tickets" src/integrations` — should not expect tickets table
3. **Visual QA** against screenshot at 1440×900
4. **Update vault docs:** append to `ui-revamp-update-2026-06-27.md`
5. **Complete side mission:** confirm delete `SIDEPLAN.md`

---

## Parallel Agent Delegation Matrix

Run these subagents **in parallel** within each phase:

| Phase | Agent A | Agent B | Agent C |
|-------|---------|---------|---------|
| **1** | Build `AppShell` + `navigation.ts` | Build `PageHeader` + breadcrumbs | Create route stubs under `routes/support/` |
| **2** | Build `TicketCard` + visual states | Build `RecentTicketsFeed` + data hook | Wire status/urgency token mapping + overdue logic |
| **3** | Extract KPI row + 3 chart widgets | Assemble `support/index.tsx` grid | Add server fn for message counts (or mock) |
| **4** | Create `FeatureShell` template | Generate 4 route pages (assignment–SLA) | Generate 4 route pages (statuses–reports) |
| **5** | Navigation wiring (+ Add New, View all) | Polish CSS + responsive grid | Legacy route migration / redirects |
| **6** | Run build + grep checks | Browser visual QA | Update vault documentation |

### Subagent prompt template

```
You are implementing [PHASE N, TASK X] for the Fridson support dashboard redesign.

Read first:
- 02-Projects/fridson/plans/01-support-dashboard-redesign.md (Phase N section)
- fridson-app/AGENTS.md
- Copy patterns from files cited in the plan

Rules:
- Work only in fridson-app/
- Use existing shadcn components and tokens
- Do not invent APIs — use Allowed APIs from Phase 0
- Reports = tickets

Deliver: working code + list of files changed + verification steps run.
```

---

## File tree (expected output)

```
fridson-app/src/
├── components/
│   ├── layout/
│   │   ├── AppShell.tsx
│   │   └── PageHeader.tsx
│   └── support/
│       ├── RecentTicketsFeed.tsx      ← P1
│       ├── TicketCard.tsx             ← P1
│       ├── FeatureShell.tsx
│       └── widgets/
│           ├── SupportKpiRow.tsx
│           ├── TicketReplyTimeChart.tsx
│           ├── TicketPriorityChart.tsx
│           └── AvgTicketsChart.tsx
├── config/
│   └── navigation.ts
└── routes/
    ├── _operator.tsx                  (layout)
    └── support/
        ├── index.tsx                  (Support Overview)
        ├── assignment.tsx
        ├── topics.tsx
        ├── sla.tsx
        ├── statuses.tsx
        ├── collaboration.tsx
        ├── email.tsx
        ├── authorization.tsx
        └── reports.tsx
```

---

## Next action

**Start Phase 1** — launch 3 parallel coder agents for AppShell, PageHeader, and route stubs. When Phase 1 verifies, proceed to **Phase 2 (P1 Recent Tickets Feed)** before finishing chart widgets.
