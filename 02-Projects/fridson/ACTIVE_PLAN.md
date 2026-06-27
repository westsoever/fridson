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
- [x] 🧑 Complete **Day 1 check-in** on [Z2D Dashboard](https://z2d-base.lovable.app/dashboard) ✅ done
- [x] 🧑 Confirm **Milestone 1** (team confirmed) ✅ done
- [x] 🧑 Redeem **Lovable credits** — code `COMM-ZD2-MAPJ` ✅ done
- [ ] 🧑 Redeem **Azure credits** ($1,000) — https://luma.link/aMPPeE5k4A
- [ ] 🧑 Upgrade to **Cursor Pro** for team usage
- [ ] 🧑 Check **Memtrace** availability on Z2D dashboard

---

## Phase 1 — Define & Validate
*Problem locked 2026-06-27. Narrow demo wedge, then build.*

- [x] 🤝 Define problem space — office lifecycle management, operating → predictive [[04-Resources/Z2D/finding-the-problem]]
- [x] 🤝 Articulate pain point — reactive maintenance, buildings wear down, no forward visibility
- [x] 🤝 Identify target user — facility managers / office servicing teams
- [x] 🤖 Pick demo wedge — **Scan/Tap/Route** (QR → issue → Slack) ✅ confirmed
- [x] 🤖 Draft MVP flow spec — scan QR → tap issue → route to in-house FM / external contractor [[MVP-FLOW]]
- [x] 🤖 Draft Lovable prompt + validation map — copy-paste build spec + Z2D scorecard [[LOVABLE-PROMPT]]
- [x] 🤝 Research existing lifecycle maintenance software — competitor gaps → [[04-Resources/Z2D/competitor-validation]] ✅
- [x] 🤝 Gather at least 2 validation signals — $2.98B market, Reddit practitioner quotes, Snapfix comp → [[04-Resources/Z2D/hackathon-strategy]] ✅
- [x] 🧑 GATE: Team agrees on demo wedge + one-sentence pitch before full build ✅ — demo live at [fridson.lovable.app](https://fridson.lovable.app)

## Phase 2 — Build MVP (Sat 13:30 – Sun ~12:00)
*QR → tap → Slack works. Now harden the demo and add the second routing path.*

- [ ] 🤖 ▶ NEXT Verify **two routing paths** visible on demo — printer/out-of-paper → in-house; bathroom/leak → contractor (different Slack channels)
- [ ] 🤖 Confirm **admin/backup page** exists — shows submitted reports if Slack is slow
- [ ] 🤖 Print/generate **5 QR codes** for demo props: printer, bathroom, meeting room, pump room, kitchen
- [ ] 🤝 Prepare **Pitch & Dine** update for Sat 20:00 — hook + live demo + validation bullets [[04-Resources/Z2D/competitor-validation]]
- [ ] 🧑 GATE: Day 1 progress demo-ready for Pitch & Dine (Sat 20:00)

## Phase 2.5 — Resolution Agent (STRETCH — only after Phase 2 must-have is solid)
*The differentiator: report → resolved. See [[RESOLUTION-AGENT]]. Gated behind a working Capture→Route demo.*

- [ ] 🧑 GATE: Capture→Route demo bulletproof before starting any agent work
- [ ] 🤖 Build **Sourcing Brief** (research only) — broken asset → 3 ranked replacement options + prices
- [ ] 🤖 Add **RFQ email** outreach — draft + send to demo vendor inbox, parse replies
- [ ] 🤖 Stretch: **AI negotiation call** to a sandbox/teammate number — the headline demo beat
- [ ] 🤖 Wire human-in-the-loop approval gate (no autonomous purchase) + audit log
- [ ] 🤝 Prepare recorded fallbacks (call clip, pre-fetched brief) so it never breaks the must-have

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
- **Azure credits** — $1,000 unclaimed (https://luma.link/aMPPeE5k4A)
- **Two-scenario demo** — need to confirm printer→in-house and bathroom→contractor routes are visually distinct
- **Pitch & Dine at 20:00** — ~4 hours to polish demo + prepare 2-min update

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
| 2026-06-27 | Product expanded — [[RESOLUTION-AGENT]] added as "Resolve" layer (research → source → negotiate replacements). Positioned as headline stretch, gated behind Capture→Route must-have |
| 2026-06-27 | Milestone 1 confirmed, Day 1 check-in done, Lovable credits redeemed — demo live at fridson.lovable.app |
| 2026-06-27 | Phase 1 complete — validation research + competitor landscape done; QR→Slack flow confirmed working |
| 2026-06-27 | Data Brain session — hero positioning shift to "24/7 AI Property Manager"; Pitch & Dine strategy: show full scope, use feedback to cut [[04-Resources/Z2D/data-brain]] |
