# Problem — Office Lifecycle Management

**Project:** [[02-Projects/z2d-lifecycle/ACTIVE_PLAN|Z2D Lifecycle Platform]] · Team Fridson
**Source:** [[04-Resources/Z2D/finding-the-problem|Finding the Problem meeting]] · 2026-06-27
**Status:** Defined — demo wedge still narrowing

---

## One-sentence pitch

> Office buildings wear down and servicing is reactive — we predict what will fail before it does, connecting sensors to a dashboard that alerts the right service team automatically.

---

## Who has the pain

**Facility managers and office servicing teams** responsible for keeping a building running: replenishment (cups, paper, water), hardware upkeep (printers, projectors), and infrastructure (plumbing, energy).

They operate in **reactive mode** — fixing things after they break, restocking when empty, responding to complaints.

---

## The pain

| Pain | Detail |
|------|--------|
| **Lifecycle cost** | Buildings deteriorate no matter how well they're treated — maintenance is an ongoing, expensive burden |
| **Reactive operations** | Teams respond to failures instead of preventing them |
| **No forward visibility** | No reliable way to know *what will happen* to assets before they fail |
| **Manual coordination** | Alerts and dispatch to service teams (cleaning, plumbing, IT) are ad hoc |

> "The problem we're solving is life cycle. It costs a lot of money… no matter how well you treat your office, it's gonna wear down."

---

## Lifecycle stages (where we sit)

1. **Design/Build** — not our focus
2. **Operating** — day-to-day building operations during its lifetime
3. **Predictive Maintenance** — knowing what's going to happen before it does

**Our wedge:** between **Operating** and **Predictive** — the building already exists; we make future failures visible early.

---

## What's novel

- **AI + sensor data** to move from reactive → predictive
- **Automated alerting** (e.g. Slack) to the relevant service team when a high-risk asset crosses a threshold
- **Demo-first scope:** one sensor, one use case, one dashboard — provable in two days

---

## Demo candidates (pick one)

| Use case | Demo fit | Risk |
|----------|----------|------|
| **Hygiene** — vision/LLM detects dirty tables, pings cafeteria | Easy to demo | Vision model complexity |
| **Plumbing / pump** — vibration or flow sensor predicts leak | Strong predictive story | Threshold calibration |
| **Office hardware** — printer/projector monitoring | Relatable | Needs more data than AI alone |
| **Energy / space** | Large market | Too broad for 2-day scope |

**Team decision:** narrow to **one sensor + one use case** (leading candidate: vibration sensor on a pump).

---

## Open (blocks build)

- Which sensor: flow, pressure, or vibration?
- What threshold indicates a future failure?
- Validation signals for pitch (market stats, competitor scan) — not yet captured

---

## Supersedes

Initial kick-off direction ("fintech credit analysis") was abandoned after team problem-finding session. See [[08-Archive/z2d-credit-analysis-pivot/project-credit-analysis]].
