# Fridson — A Suite of AI Employees for Property Management

Team Fridson · Z2D Cohort #3 · Copenhagen · 27–28 Jun 2026

A tenant scans a broken asset and taps the problem — Fridson writes a structured report, pinpoints it on the building schematic, picks the right contractors, gets bids, negotiates, and books the repair. The property manager only approves.

**Source of truth:** [[06-Wiki/decisions/2026-06-27-final-commitment|Final Commitment]]
**Active plan:** [[ACTIVE_PLAN]] · **Build roadmap:** [[ROADMAP]] · **Resolution Agent:** [[RESOLUTION-AGENT]] · **Email integration:** [[email-integration]] · **MVP flow:** [[MVP-FLOW]] · **Lovable prompt:** [[LOVABLE-PROMPT]] · **Problem:** [[06-Wiki/Problem]] · **Team:** [[team]]

**Live demo:** [fridson.lovable.app](https://fridson.lovable.app) · hero QR: `/r/meeting-4f`

## Repos & workspace
Two separate repos live side by side in this workspace:
- **Knowledgespace** (this vault) — `github.com/westsoever/fridson` — planning, maps, team plans, docs.
- **The app** — `github.com/westsoever/fridson-app` — cloned at `fridson-app/` (Lovable-connected; Vite + React + TS + Bun + Supabase).

Agents working in this vault can directly edit `fridson-app/`. The app folder is git-ignored here and keeps its own git history — commits inside `fridson-app/` push to the app repo (and reach Lovable). Don't mix the two. Details in root `CLAUDE.md → The app code lives here too`.

---

## Where to look
- **What to build next →** [[ROADMAP]] (sequenced build backlog with acceptance criteria)
- **Phases, gates & demo arc →** [[ACTIVE_PLAN]]
- **Execution plans →** [[plans/README|plans/00–09]]
- **Post-deploy verify →** [[plans/LIVE-VERIFY-RUNBOOK]]
- **Post-demo validation →** ACTIVE_PLAN Phase 8 (The Shack mapping + office-manager calls)

---

## Shipped (overnight 28 Jun)

**App (`fridson-app` `be24035` on `origin/main`):**
- Approve → resolution agent → mock RFQ inbox redirect (`AGENT_MOCK_INBOX` + Resend)
- Cobalt UI revamp — dashboard KPIs, workspace triage, Manrope/Sora fonts, chart polish
- Operator onboarding tour — first-launch walkthrough with Skip/Back/Next ([[plans/09-operator-onboarding-tour]])
- Activity feed — promoted in sidebar; vertical timeline on `/projection`
- Stakeholder context panel, schematic floor selector, system map linear flow

**Vault & logistics:**
- Execution plans 00–07 + live verify runbook + deploy blocker report
- Milestone 2 submitted (15:00) · MVP QR printed · demo hardware confirmed · Day 2 check-in done
- Phase 8 filed — real office inventory, The Shack floorplan, validation calls

---

## Blockers

**Deployment (demo-critical — unlocks live agent + real projection feed):**
- [x] 🌐 **Push app to Lovable** — ✅ `be24035` on `origin/main`
- [ ] 🔑 **Lovable Supabase sync OR CLI** — apply 7 migrations + deploy `agent`/`process-triage`/`process-research`; see [[plans/DEPLOY-BLOCKER-REPORT]] (CLI 403 without project-scoped token)
- [ ] 🔑 **Set function secrets** — `LOVABLE_API_KEY`, `FIRECRAWL_API_KEY`, `RESEND_API_KEY`, `AGENT_MOCK_INBOX=<team inbox>`
- [ ] 🖥️ **Live verify** — [[plans/LIVE-VERIFY-RUNBOOK]] (hero scan → Approve → RFQ inbox → projection `?feed=real`)

**Human logistics (Sun 28 Jun):**
- [x] 🧑 **Demo hardware** — presenter, projector, phone on same network ✅
- [x] 🧑 **Day 2 check-in** — Z2D dashboard ✅
- [x] 🧑 **QR prints (MVP)** — hero `meeting-4f` + MVP props from [[pitch/qr-codes]] ✅
- [x] 🧑 **Milestone 2 (15:00)** — submitted on Z2D dashboard ✅
- [ ] 🧑 **Full dry-run (before 16:00)** — [[pitch/dry-run-checklist]]
- [ ] 🧑 **Live demo & judging** — 16:00

**Decisions / cleanup:**
- [ ] ❓ **Dangling vault remote** `fridson-app → westsoever/fridson-app` — remove?
