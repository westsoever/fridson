# Z2D Lifecycle Platform — Team Fridson

**Goal:** Ship a demoable predictive office lifecycle platform — sensor → dashboard → automated alert — that scores on all four Z2D judging criteria by Sunday 28 June 2026, 16:00 CEST.
**Deadline:** Sun 28 Jun 2026 · 16:00 live demo · 15:00 submission
**Owner:** Team Fridson (Shuhia, Chris, Lennert)

**Problem definition:** [[06-Wiki/Problem|Office Lifecycle Management]]

---

## Session Protocol
- 🤖 Claude can do autonomously
- 🤝 Claude drafts, human reviews
- 🧑 Human-only action required
- Never skip a GATE — these are explicit checkpoints requiring sign-off

## Decision Framework (Z2D Judging)
Before any major decision, score against:
1. **PRODUCT** — Does this make the product stronger and more functional?
2. **PROBLEM** — Does it sharpen a real pain point in a novel way?
3. **VALIDATION** — Does it add evidence of market demand?
4. **SPEED & DEMO** — Does it move us toward a catchy demo by Sun 16:00?

Flag the weakest criterion after each review and prioritize it next.

## Human-Action Queue
- [ ] 🧑 Complete **Day 1 check-in** on [Z2D Dashboard](https://z2d-base.lovable.app/dashboard)
- [ ] 🧑 Confirm **Milestone 1** (team confirmed) by Sat 14:00
- [ ] 🧑 Redeem **Lovable credits** — code `COMM-ZD2-MAPJ` → lovable.dev → Settings → Plans & Credits → Pro Plan 1
- [ ] 🧑 Redeem **Azure credits** ($1,000) — https://luma.link/aMPPeE5k4A
- [ ] 🧑 Upgrade to **Cursor Pro** for team usage
- [ ] 🧑 Check **Memtrace** availability on Z2D dashboard

---

## Phase 1 — Define & Validate
*Problem locked 2026-06-27. Narrow demo wedge, then build.*

- [x] 🤝 Define problem space — office lifecycle management, operating → predictive [[04-Resources/Z2D/finding-the-problem]]
- [x] 🤝 Articulate pain point — reactive maintenance, buildings wear down, no forward visibility
- [x] 🤝 Identify target user — facility managers / office servicing teams
- [ ] 🤖 ▶ NEXT Pick demo wedge — **[[MVP-FLOW|Scan/Tap/Route]]** (QR → issue → Slack) *or* one sensor + one use case (vibration/pump vs hygiene)
- [x] 🤖 Draft MVP flow spec — scan QR → tap issue → route to in-house FM / external contractor [[MVP-FLOW]]
- [x] 🤖 Draft Lovable prompt + validation map — copy-paste build spec + Z2D scorecard [[LOVABLE-PROMPT]]
- [ ] 🤝 Research existing lifecycle maintenance software — pitch data + competitor gaps (#3)
- [ ] 🤝 Gather at least 2 validation signals — stats, mentor quote, or market evidence
- [ ] 🧑 GATE: Team agrees on demo wedge + one-sentence pitch before full build

## Phase 2 — Build MVP (Sat 13:30 – Sun ~12:00)
*Sensor → dashboard → alert. Mentors on-site Sat afternoon.*

- [ ] 🤖 Build basic **HTML dashboard** to visualize asset alerts
- [ ] 🤖 Connect high-risk asset to dashboard (sensor data or simulated feed)
- [ ] 🤖 Implement **automated alert** trigger (e.g. Slack ping to service team)
- [ ] 🤖 Wire demo data so judges can see threshold breach → alert flow live
- [ ] 🤝 Prepare **Pitch & Dine** update for Sat 20:00 — problem + live demo path
- [ ] 🧑 GATE: Day 1 progress demo-ready for Pitch & Dine (Sat 20:00)

## Phase 3 — Polish & Demo (Sun ~09:00–16:00)
*Submission → live demo → judging.*

- [ ] 🧑 Complete **Day 2 check-in** on Z2D dashboard
- [ ] 🤖 Harden demo path — no dead ends, fast load, clear UI
- [ ] 🤝 Write demo script: hook → problem → product → validation → ask (catchy & entertaining)
- [ ] 🤝 Final submission prep — **Milestone 2 by Sun 15:00**
- [ ] 🧑 GATE: Dry-run demo with team before Sun 16:00
- [ ] 🧑 Live demo & judging — Sun 16:00

---

## Event Schedule (reference)

### Sat 27 Jun
| Time | Event |
|------|-------|
| 09:00 | Doors open |
| 09:30 | Team formation & kick-off |
| 13:00 | Lunch |
| 13:30 | Building (mentors on-site) |
| **14:00** | **Milestone 1 — team confirmed** |
| 20:00 | Pitch & Dine — Day 1 progress |
| 22:00 | Day 1 wrap |

### Sun 28 Jun
| Time | Event |
|------|-------|
| 09:00 | Doors open |
| **15:00** | **Milestone 2 — submission done** |
| **16:00** | **Live demos & judging** |
| 18:00 | Winner announcement |

---

## Team & Resources

### Team Fridson (3/5)
| Member | Email | Role |
|--------|-------|------|
| Shuhia | shuhia.on@gmail.com | admin |
| Chris | chrisw0129@gmail.com | member |
| Lennert | jessenlennert@outlook.com | member |

### Credits & Tools
| Resource | Status | Details |
|----------|--------|---------|
| Cursor | ✅ claimed | upgrade to Pro for team |
| Lovable | ⏳ redeem | code `COMM-ZD2-MAPJ` |
| Azure | ⏳ redeem | $1,000 — https://luma.link/aMPPeE5k4A |
| Memtrace | ⏳ check | Z2D dashboard |
| Claude Code | active | Sonnet 4.6, high effort |

### Fellowship prize (top teams)
$25,000 cloud credits · Copenhagen workspace (The Shack, Antler, Microsoft) · ongoing mentorship

---

## Blockers
- **Demo wedge open** — Scan/Tap/Route leading; team must confirm vs sensor dashboard before full build
- **Validation empty** — no market stats or competitor research captured yet
- **Dashboard check-ins pending** — Day 1 and Milestone 1 (Sat 14:00) not completed
- **Lovable build pending** — [[LOVABLE-PROMPT]] ready; needs credits redeemed + Slack webhooks configured

---

## Status Log
| Date | Summary |
|------|---------|
| 2026-06-27 | Project created from inbox — initial direction: fintech credit analysis |
| 2026-06-27 | Problem pivot — team locked office lifecycle / predictive maintenance ([[04-Resources/Z2D/finding-the-problem]]) |
| 2026-06-27 | Merged to main; problem defined in [[06-Wiki/Problem]]; project renamed to z2d-lifecycle |
| 2026-06-27 | Wrap-up: inbox processed; blockers captured in README; next: pick sensor + use case, build dashboard |
| 2026-06-27 | MVP flow designed — [[MVP-FLOW]] (scan QR → tap issue → Slack to FM/contractor); demo wedge decision still open |
| 2026-06-27 | Lovable prompt + validation map drafted — [[LOVABLE-PROMPT]]; app host locked to Lovable; next: send prompt, configure Slack, team lock wedge |
