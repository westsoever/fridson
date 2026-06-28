# Fridson — A Suite of AI Employees for Property Management

Team Fridson · Z2D Cohort #3 · Copenhagen · 27–28 Jun 2026

A tenant scans a broken asset and taps the problem — Fridson writes a structured report, pinpoints it on the building schematic, picks the right contractors, gets bids, negotiates, and books the repair. The property manager only approves.

**Source of truth:** [[06-Wiki/decisions/2026-06-27-final-commitment|Final Commitment]]
**Active plan:** [[ACTIVE_PLAN]] · **Build roadmap:** [[ROADMAP]] · **Resolution Agent:** [[RESOLUTION-AGENT]] · **MVP flow:** [[MVP-FLOW]] · **Lovable prompt:** [[LOVABLE-PROMPT]] · **Problem:** [[06-Wiki/Problem]] · **Team:** [[team]]

**Live demo:** [fridson.lovable.app](https://fridson.lovable.app)

## Repos & workspace
Two separate repos live side by side in this workspace:
- **Knowledgespace** (this vault) — `github.com/westsoever/fridson` — planning, maps, team plans, docs.
- **The app** — `github.com/westsoever/fridson-app` — cloned at `fridson-app/` (Lovable-connected; Vite + React + TS + Bun + Supabase).

Agents working in this vault can directly edit `fridson-app/`. The app folder is git-ignored here and keeps its own git history — commits inside `fridson-app/` push to the app repo (and reach Lovable). Don't mix the two. Details in root `CLAUDE.md → The app code lives here too`.

---

## Where to look
- **What to build next →** [[ROADMAP]] (sequenced build backlog with acceptance criteria)
- **Phases, gates & demo arc →** [[ACTIVE_PLAN]]
- **Execution plans →** [[plans/README|plans/00–07]]

---

## Blockers

**Deployment (demo-critical):**
- [ ] 🔑 **Apply migrations + deploy edge functions** — CLI 403 without `SUPABASE_ACCESS_TOKEN`; see [[plans/DEPLOY-BLOCKER-REPORT]]
- [ ] 🔑 **Set function secrets** — `LOVABLE_API_KEY`, `RESEND_API_KEY`, `AGENT_MOCK_INBOX=<team inbox>` on `agent` function
- [ ] 🌐 **Push app changes to Lovable** — approve→agent→email workflow wired locally (uncommitted in `fridson-app/`); must push + deploy before live verify
- [ ] 🖥️ **Stage feed** — `/projection?feed=real` on demo laptop; confirm Realtime on `events`

**Human logistics (Sun 28 Jun):**
- [ ] 🧑 **QR prints + hardware** — [[pitch/qr-codes]] · phone + projector same network
- [ ] 🧑 **Milestone 2 (15:00)** — [[pitch/milestone-2-copy]]
- [ ] 🧑 **Full dry-run (before 16:00)** — [[pitch/dry-run-checklist]]
- [ ] 🧑 **Demo hardware** — presenter, projection placement, same Wi-Fi

**Decisions / cleanup:**
- [ ] ❓ **Dangling vault remote** `fridson-app → westsoever/fridson-app` — remove?
- [ ] 🌐 **Push vault to origin** — knowledgespace `main` has unpushed plan + wrap-up edits
