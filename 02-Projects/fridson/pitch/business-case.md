# Business Case — Minute 3 (Source of Truth for the Numbers)

**Owner:** Track 4 (Pitch) · **Status:** Locked for Sun demo
**Use:** This is the canonical source for every number spoken in the pitch. `script.md` references these; do not invent numbers elsewhere.
**Anchors:** [[ACTIVE_PLAN]] Phase 6 · [[06-Wiki/decisions/2026-06-27-final-commitment]] (Minute 3 + "80% quality" framing) · [[04-Resources/Z2D/hackathon-strategy]] · [[04-Resources/Z2D/competitor-validation]] · [[05-Knowledge/pricing/ai-property-management-pricing-research]]

> **The framing (from source of truth):** *"If we can reduce cost and do it way faster while achieving 80% of the quality — that is still a win."*

---

## The market it plays in (context, not a headline number)

Facility-management software is a **$2.98B market in 2026, growing to $4.95B by 2031 at 10.68% CAGR** (Mordor Intelligence).[^market] The budget and category are already validated by incumbents (Planon, MaintainX, Snapfix, Infraspeak). Fridson does not claim that market — it claims the **coordination layer inside it** that those tools leave on the property manager's desk.

The documented time-sink we attack: facility issues still arrive as *"hallway conversations, sticky notes, phone calls, and emails,"* creating missed jobs and unclear priorities,[^maintainx] and practitioners confirm tenants *"leave out vital detail information."*[^reddit] The expensive part — sourcing, getting bids, and negotiating a high-cost repair/replacement — is hours of skilled PM time per case.

---

## The 3 defensible numbers (the Minute-3 slide)

### 1. COST ↓ — **15–25% lower operating cost ≈ DKK 140k–320k/year per building**

Fridson removes the coordination labor a property manager spends on intake, triage, routing, vendor follow-up, and sourcing — **0.3–0.7 FTE** of property-coordination time per building.[^pricing-fte]

- **Per high-cost resolution:** manual sourcing (identify product → contact ~3 vendors → collect quotes → compare → negotiate → book) is **~2–3 hours of PM time** at **DKK 287/hr**[^salary-pm] ≈ **DKK 575–860 per case**. With Fridson the PM does one thing — *approve* (~5 min ≈ DKK 24). That is a **~95% cut in coordination cost on the cases that actually cost money.**
- **At building scale:** 0.3–0.7 FTE of a facilities coordinator (gross DKK 349,852/yr, ERI;[^salary-coord] ~1.3× fully loaded ≈ DKK 455k) ≈ **DKK 140k–320k/year saved**, i.e. a **15–25% operational cost reduction** — squarely in line with the AI-property-management benchmark of *15–25% operational cost reductions*.[^elise]
- **Net of price:** the managed pilot is **DKK 25,000/month (DKK 300k/yr) for 10 areas**;[^pricing-offer] the labor saving alone is in the same range *before* counting better-negotiated vendor prices, so the customer breaks even on coordination time and keeps the procurement savings.

> **Assumptions:** PM/coordinator spends **≥10 hrs/week** on issue coordination (the pricing-credibility threshold[^pricing-fte]); Copenhagen loaded labor rates per ERI/SalaryExpert; one building / 10 areas; vendor repair/replacement spend billed directly and excluded from this figure.

### 2. TIME ↓ — **resolution cycle from ~3–5 days → same-day (decision-ready in minutes)**

The bottleneck in a high-cost repair is not the fix — it is the **waiting and chasing**: vague report → PM triage → find vendors → email/call → wait for quotes → compare → book. That round-trip is typically **3–5 business days**.

- Fridson collapses the human-coordination portion to **minutes**: the structured report is instant (asset · location · issue), the agent queries the contractor directory, sends RFQs, negotiates within set bounds, and surfaces a **decision-ready recommendation + proposed slot** — the projected demo runs this in **~60 seconds**. The PM approves the same day.
- **≈80% faster time-to-action**, consistent with the AI-property-management benchmark of *up to 80% lead-response improvement*.[^elise] Capture itself goes from a vague email to a *"3-second work order"* (Snapfix's own positioning for the category).[^snapfix]

> **Assumptions:** 3–5 day manual baseline is a stated estimate for a high-cost repair requiring sourcing + multi-vendor quotes (not a cited figure); "minutes / same-day" is the demonstrated agent path with human approval; emergency out-of-hours cases excluded.

### 3. QUALITY — **~80% of expert quality, 100% human approval on spend, at ~1/5 the management cost**

The tradeoff, stated honestly: the agent does not need to beat a veteran property manager — it needs to capture **~80% of the quality** while being dramatically cheaper and faster, with the human keeping the final call.

- **Cost ratio:** AI-managed operations are priced around **3.9% of gross** vs **20–35% for traditional full-service management** (TIDY benchmark)[^tidy] — roughly **one-fifth the management cost** for the coordination layer.
- **Risk is contained:** the PM approves/disapproves **every** spend; the agent never purchases autonomously, stays within FM-set negotiation bounds, and logs a full audit trail.[^resolution] So "80% quality" carries no downside on money — the 20% the human keeps is exactly the judgment call.
- **The win:** a task that took **~3 days and ~3 hours of skilled labor** now takes **minutes and one tap**. 80% quality + cheaper + faster = a win.

> **Assumptions:** "80% quality" is the team's accepted demo-quality bar (source of truth), not a measured benchmark; cost-ratio is short-term-rental-derived (TIDY) and used as a directional pattern, not a like-for-like commercial-FM figure.

---

## One-slide summary (for the deck)

| Lever | Number | Anchored to |
|---|---|---|
| **Cost ↓** | **15–25% lower op-cost ≈ DKK 140–320k/yr** (0.3–0.7 FTE) | EliseAI 15–25%[^elise] · ERI/SalaryExpert labor[^salary-pm][^salary-coord] · pricing doc[^pricing-fte] |
| **Time ↓** | **~3–5 days → same-day; decision-ready in minutes (~80% faster)** | EliseAI up to 80% lead-response[^elise] · Snapfix "3-second"[^snapfix] |
| **Quality** | **~80% quality · 100% human-approved spend · ~1/5 mgmt cost** | TIDY 3.9% vs 20–35%[^tidy] · approval guardrails[^resolution] |

**Market frame:** $2.98B → $4.95B FM-software market;[^market] Fridson owns the coordination layer inside it.

**≤60s narration:** "The facility-software market is $2.98 billion and growing — but the expensive part still sits on the property manager: triaging vague reports and chasing vendors for quotes. Fridson cuts that coordination cost 15 to 25% — roughly DKK 140 to 320 thousand a year per building, about half a full-time role. It takes a high-cost repair from three-to-five days down to same-day, with a decision-ready recommendation in minutes. The agent isn't perfect — call it 80% of an expert — but the human approves every cent, it costs about a fifth of traditional management, and it's far faster. 80% quality, cheaper, faster: that's a win."

---

## Sources

[^market]: Mordor Intelligence — Facility Management Software Market: $2.98B (2026) → $4.95B (2031), 10.68% CAGR. https://www.mordorintelligence.com/industry-reports/facility-management-software-market
[^elise]: EliseAI AI property-management cost guide — 15–25% operational cost reductions; up to 80% lead-response improvement. https://eliseai.com/blog/ai-property-management-software-costs
[^tidy]: TIDY property-management fee benchmark — AI-managed ≈3.9% of gross vs 20–35% traditional full-service. https://www.tidy.com/property-management-fees
[^salary-pm]: SalaryExpert — Property manager, Denmark ≈ DKK 596,870/yr (≈ DKK 287/hr). https://www.salaryexpert.com/salary/job/property-manager/denmark
[^salary-coord]: ERI — Facilities coordinator, Denmark ≈ DKK 349,852/yr (≈ DKK 168/hr). https://www.erieri.com/salary/job/facilities-coordinator/denmark
[^snapfix]: Snapfix — "the home of the 3-second work order." https://www.snapfix.com/
[^maintainx]: MaintainX — facility requests arrive via "hallway conversations, sticky notes, phone calls, and emails." https://www.getmaintainx.com/blog/facility-maintenance-examples-7-cmms-success-stories
[^reddit]: r/FacilityManagement — service email "works OK" but tenants "leave out vital detail information." https://www.reddit.com/r/FacilityManagement/comments/1mnej2o/would_a_qrbased_issue_reporting_tool_save_you/
[^pricing-fte]: [[05-Knowledge/pricing/ai-property-management-pricing-research]] — 0.3–0.7 FTE saving justifies DKK 25–45k/month; ≥10 hrs/week coordination = credible.
[^pricing-offer]: [[05-Knowledge/pricing/ai-property-management-pricing-research]] — recommended pilot: DKK 25,000/month + DKK 15,000 setup for 10 areas.
[^resolution]: [[02-Projects/fridson/RESOLUTION-AGENT]] — human-in-the-loop guardrails: no autonomous purchase, FM-set negotiation bounds, full audit trail, AI disclosure.
