# Pricing Research — AI Property Management Service

Created: 2026-06-27  
Context: Fridson / Copenhagen pilot pricing

## Executive recommendation

For an **AI property management service that automates and handles the workflow of a property manager**, the strongest pricing model is not pure SaaS per user. The buyer is not just buying software; they are buying **reduced coordination work, faster response, better documentation, and fewer avoidable failures**.

Recommended pilot pricing for **10 building areas in Copenhagen**:

| Package | Best for | Monthly price | Setup fee | What is included |
|---|---|---:|---:|---|
| **Pilot — AI Workflow Layer** | 10 areas in one building or campus | **DKK 12,000–18,000 / month** | **DKK 7,500–15,000** | QR reporting, routing rules, dashboard, Slack/email alerts, issue log, weekly summary |
| **Managed Ops — AI + Human Oversight** | Customer wants Fridson to actively coordinate tasks | **DKK 25,000–45,000 / month** | **DKK 15,000–35,000** | Everything in Pilot + human review, vendor coordination, SLA follow-up, monthly owner report |
| **Full Resolution Service** | Customer wants issue-to-resolution workflow | **DKK 45,000–90,000 / month** | **DKK 30,000–75,000** | Everything above + vendor sourcing, RFQs, quote comparison, replacement recommendations, audit trail |

Recommended hackathon/commercial wedge:

> **Start at DKK 25,000/month for 10 areas** as a managed AI property-operations pilot, plus a DKK 15,000 setup fee.

This is high enough to avoid being seen as “just another maintenance app,” but low enough to be cheaper than hiring even one extra full-time property/facility coordinator in Copenhagen.

## Benchmark evidence

### 1. Software-only maintenance tools are cheap per user

| Product | Public pricing signal | Relevant notes |
|---|---:|---|
| **MaintainX** | Free, then **$20/user/month Essential**, **$65/user/month Premium**, Enterprise custom | Requester users are free; Premium includes analytics, purchase orders, API, external work orders; Enterprise adds IoT, asset health, escalation protocols, SSO, and AI CoPilot. |
| **UpKeep** | **$24/user/month Essential**, **$55/user/month Premium**, Professional/Enterprise custom | Includes Nova AI from Essential; higher tiers add automation, integrations, governance. Implementation packages range from **$500–$5,000**. |
| **Snapfix** | Pricing not publicly listed; sales/demo flow | Product is close to Fridson’s wedge: photo/QR work orders, task management, traffic-light status, facility/property management. |
| **Facilio** | Custom quote | Enterprise facility-management packaging; modules include work orders, preventive maintenance, vendor RFQs, compliance, tenant portals, SSO, and audit controls. |

Implication: if Fridson prices as software-only, it gets compared to **$20–$65/user/month** tools. That is the wrong anchor for the full vision.

Better anchor:

> Fridson is not only a work-order app. It is an **AI property manager workflow layer** that reduces human coordination hours.

### 2. AI property management uses different pricing models

AI property-management vendors commonly use:

- **Per-unit monthly pricing**
- **Tiered pricing by portfolio size or feature set**
- **Flat enterprise monthly fees**
- **Transaction or usage fees** for premium workflows
- **Implementation fees** for migration, integrations, and training

EliseAI’s AI property-management cost guide identifies per-unit monthly pricing as common and notes ROI benchmarks such as **15–25% operational cost reductions**, up to **80% lead-response improvement**, and maintenance coordination savings from optimized scheduling and communication.

Implication: Fridson can justify pricing against **operational savings**, not seat count.

### 3. AI-managed service can undercut traditional human service

TIDY’s property-management fee benchmark positions AI management at **3.9% of gross bookings** with a **$39/month minimum**, compared with traditional full-service property management at **20–35% of gross bookings**, and half-service/cohosting at **10–15%**. This is short-term-rental oriented, not commercial FM, but it gives a useful pricing pattern:

> AI-managed operations are priced as a lower-cost alternative to human-heavy management, not as a cheap SaaS tool.

Implication for Fridson: price as a **managed automation service** at a fraction of the cost of adding operational headcount.

### 4. Copenhagen labor costs support a managed-service price

Public salary benchmarks suggest Danish/Copenhagen property and facility operations labor is expensive:

| Role | Benchmark signal |
|---|---:|
| **Property manager, Denmark** | SalaryExpert reports average gross salary around **DKK 596,870/year**, or **DKK 287/hour**. |
| **Property manager, Copenhagen** | ERI reports average range around **DKK 442,192–773,836/year**. |
| **Maintenance technician, Copenhagen** | SalaryExpert reports average gross salary around **DKK 479,964/year**, or **DKK 231/hour**. |
| **Facilities coordinator, Denmark** | ERI reports average pay around **DKK 349,852/year**, or **DKK 168/hour**. |

A fully loaded employee cost is higher than gross salary once employer costs, vacation, sickness, equipment, admin, and management overhead are included.

Implication: if Fridson saves only **0.3–0.7 FTE** of facility/property coordination time, a **DKK 25,000–45,000/month** managed service can be economically credible.

## Recommended pricing architecture

### A. Charge by building area for the wedge

This is easiest for the customer to understand during a pilot.

| Tier | Price | Included areas | Good for |
|---|---:|---:|---|
| **Starter** | DKK 9,000/month | Up to 5 areas | Small office pilot |
| **Pilot 10** | **DKK 18,000/month** | Up to 10 areas | Hackathon/customer discovery pilot |
| **Ops 25** | DKK 35,000/month | Up to 25 areas | Multi-floor office or small portfolio |
| **Portfolio** | Custom from DKK 60,000/month | 50+ areas / multi-site | Larger asset manager / landlord |

Add setup:

| Setup item | Price |
|---|---:|
| QR/asset mapping | DKK 5,000–15,000 |
| Slack/email/Teams routing setup | DKK 5,000–10,000 |
| Admin dashboard + report template | DKK 5,000–15,000 |
| Total setup range | **DKK 15,000–35,000** |

### B. Separate software from managed operations

| Layer | What customer buys | Pricing logic |
|---|---|---|
| **Software layer** | QR reporting, dashboard, routing, logs | Per area / per building / per site |
| **AI workflow layer** | Classification, summaries, routing recommendations, recurring-issue detection | Included in higher tier or usage allowance |
| **Managed service layer** | Human-in-loop vendor coordination, follow-ups, reports | Monthly retainer |
| **Resolution layer** | Sourcing brief, RFQ, vendor quote comparison, negotiation support | Per resolution or included allowance |

### C. Charge extra for high-value resolution work

The Resolution Agent should not be bundled cheaply. It creates direct measurable savings on replacement/procurement work.

| Resolution service | Suggested price |
|---|---:|
| Sourcing brief for broken/high-cost asset | DKK 750–1,500 per brief |
| Vendor RFQ + quote comparison | DKK 1,500–3,500 per case |
| Negotiated replacement workflow | 5–10% of verified savings, or DKK 3,000–7,500 per case |
| Emergency/out-of-hours coordination | Premium add-on |

## Pricing for “10 building areas in Copenhagen”

Assumption: 10 areas are rooms/assets/zones in one office building or campus, not 10 separate buildings. Cleaning, security, and specialist repair labor are excluded and billed directly by vendors.

### Suggested pilot offer

**Name:** Fridson AI Property Manager — 10-Area Pilot  
**Price:** **DKK 25,000/month**  
**Setup:** **DKK 15,000 one-time**  
**Term:** 60–90 days  
**Scope:**

- Map 10 building areas/assets
- Generate QR reporting pages
- Configure issue categories and routing rules
- Slack/email/Teams alerts to in-house team and contractors
- Admin dashboard / report log
- Weekly issue summary
- Monthly stakeholder report
- Human-in-loop QA on routing and vendor follow-up
- 3 included resolution briefs per month

### Why DKK 25,000/month is defensible

It is framed against labor and operational savings:

- Cheaper than hiring one full-time facility/property coordinator.
- Can save property manager time by reducing manual intake, triage, and follow-up.
- Creates documentation that owners, insurers, and compliance stakeholders value.
- Generates data for recurring-problem analysis and preventive maintenance.
- Provides a clear path to expansion: more areas, more buildings, resolution workflows, predictive sensors.

## Price positioning options

### Option 1 — Low-friction SaaS pilot

**DKK 12,000–18,000/month**  
Best if the customer has their own FM team and only wants intake/routing automation.

Risk: gets compared to CMMS pricing.

### Option 2 — Recommended managed AI ops pilot

**DKK 25,000–45,000/month**  
Best if Fridson actively handles workflow and coordination.

This is the preferred positioning.

### Option 3 — Outcome-priced resolution service

Base platform + **per-case resolution fees** or **share of savings**.

Best once the Resolution Agent is credible and can show actual vendor/time/cost savings.

## Sales narrative

Do not say:

> “We are a facility management app.”

Say:

> “We are an AI property manager that captures every issue, routes it to the right responder, documents the workflow, and increasingly resolves tasks before they become expensive.”

Short pricing justification:

> “For 10 areas, we charge DKK 25,000/month because we replace a large part of the coordination layer that normally sits on the property manager: issue intake, triage, routing, vendor follow-up, and reporting. Traditional tools charge per user; Fridson is priced against hours saved, faster resolution, and better asset documentation.”

## Recommended next test

In customer discovery, ask property/facility managers three pricing questions:

1. “How many hours per week do you spend triaging and following up on building issues?”
2. “What would it be worth if 60–80% of issue intake and routing happened automatically?”
3. “Would you rather pay per building, per area/asset, or as a monthly managed-service retainer?”

If they spend 10+ hours/week on coordination, the managed AI ops price is credible.

## Sources

- MaintainX pricing page: https://www.getmaintainx.com/pricing
- UpKeep pricing page: https://upkeep.com/pricing/
- Snapfix pricing/product pages: https://snapfix.com/pricing
- Facilio pricing page: https://facilio.com/pricing/
- EliseAI AI property management cost guide: https://eliseai.com/blog/ai-property-management-software-costs
- TIDY property management fee benchmark: https://www.tidy.com/property-management-fees
- SalaryExpert property manager Denmark benchmark: https://www.salaryexpert.com/salary/job/property-manager/denmark
- SalaryExpert maintenance technician Copenhagen benchmark: https://www.salaryexpert.com/salary/job/maintenance-technician/denmark/copenhagen
- ERI property manager Copenhagen benchmark: https://www.erieri.com/salary/job/property-manager/denmark/copenhagen
- ERI facilities coordinator Denmark benchmark: https://www.erieri.com/salary/job/facilities-coordinator/denmark
