---
type: analysis
date: 2026-06-27
project: "[[02-Projects/z2d-lifecycle/ACTIVE_PLAN|Z2D Lifecycle Platform]]"
related: "[[06-Wiki/Problem|Problem — Office Lifecycle Management]]"
status: current
---

# Problem Analysis — Office Lifecycle Management

> Team Fridson · Z2D Cohort #3 · Demo Sun 28 Jun 16:00

## Core problem statement

Office buildings wear down and servicing is reactive — there is no reliable way to know what will fail before it does, and high friction in reporting means issues go unnoticed until they become expensive emergencies.

---

## Who has the pain

### Facility managers
Responsible for the whole building. Overwhelmed by reactive tickets. No early warning system. Rely on physical rounds and occupant complaints to find problems.

### Servicing teams
Cleaning, plumbing, IT repair, HVAC contractors. Dispatched too late, with too little context. No structured channel to receive or acknowledge jobs.

### Building occupants
Notice issues first — broken printer, dirty bathroom, leaking tap — but have no frictionless way to report them. So they don't bother.

---

## Pain points

| Pain | What actually happens | Frequency | Severity | Business impact |
|------|-----------------------|-----------|----------|-----------------|
| **Reactive operations** | Teams fix things after they break. Failures are surprises — no proactive inspection catches wear early. | Daily | High | Unplanned downtime, emergency call-out costs, tenant complaints |
| **No forward visibility** | No signal tells a FM what will fail next week. Assets are treated as identical until one breaks. | Always | High | Cannot prioritise, cannot pre-order parts, cannot schedule labour |
| **High friction reporting** | Employees who notice problems have no easy way to report them. Email is effort. They stop reporting. | Daily | Medium | Issues compound silently; FM is last to know |
| **Manual coordination** | Routing to the right person (in-house vs. contractor) happens over WhatsApp. No log, no SLA. | Every incident | Medium | Slow response, duplicated effort, no accountability |
| **Lifecycle cost accumulation** | Deferred maintenance compounds. A pump that vibrates for weeks becomes a flood. | Ongoing | High | Accelerated asset depreciation, higher capex replacement cycle |

---

## Current state vs. desired state

| Moment | Today (broken) | With our product |
|--------|----------------|------------------|
| Issue occurs | Nobody notices — or someone reports it days later by email | Anyone scans a QR sticker, taps the issue in 3 seconds |
| Routing | FM decides manually who to call. WhatsApp message gets lost | System routes instantly: in-house FM or external contractor |
| Awareness | FM learns about problems from complaints or physical rounds | Alerts fire before failure — sensor threshold or pattern detected |
| Asset health | Unknown until breakdown. No historical record per asset | Each asset has an issue log; trend visible on dashboard |
| Contractor dispatch | Phone call, manual coordination, no record of what was done | Structured message with context; contractor receives in Slack |

---

## Why existing tools don't solve it

| Tool / approach | Category | What's missing |
|-----------------|----------|----------------|
| **Planon / Facilio** | Enterprise CMMS | Six-figure licence, 6-month implementation. Zero SMB penetration. No instant reporting by building occupants. |
| **WhatsApp / Email** | Current workaround | No structure, no routing, no audit trail, no history per asset. |
| **Google Forms** | Ad-hoc intake | No location context, no routing logic, no Slack integration, no asset history. |
| **IoT sensor platforms** | Sensor data only | No human-reported issues layer. Sensors miss anything physical or visible. |

---

## What's novel

### Zero-friction reporting
QR sticker on any asset. Camera scan → context page → one tap. No login, no app install, no form. Anyone in the building reports in 3 seconds.

### Intelligent routing
Issue type determines recipient automatically — in-house FM for replenishment and minor hardware, external contractor for plumbing, HVAC, or electrical. Right person, right channel, instantly.

### Predictive layer (Phase 2)
Sensor data (vibration, flow, pressure) feeds a threshold model. Alert fires before failure — not after. Human-reported issues + sensor signals give a complete picture of asset health.

---

## Z2D judging readiness

| Criterion | Status | Assessment |
|-----------|--------|------------|
| **PRODUCT** | Strong | Three-tap mobile flow, no install. Judges can try it live on their phone in under 10 seconds. |
| **PROBLEM** | Strong | Real pain: every office building needs FM. Reactive → predictive is the clear market direction. |
| **VALIDATION** | Needs work | Gap: no market stats or customer quotes captured yet. Add 2 signals before pitch. |
| **SPEED & DEMO** | Strong | Buildable in hours: QR pages + Slack webhook. Slack fires on projector while judge holds phone. |

> **Action needed:** Validation is the weakest criterion. Before the pitch — add at least 2 signals: a market stat (FM software market size or reactive vs. predictive cost delta) and one quote from a real facility manager or building owner.

---

## Summary

| | |
|-|-|
| **Primary user** | Facility managers |
| **Market** | Office buildings, SMB–Enterprise |
| **Demo wedge** | Scan → Tap → Route |
| **Open blocker** | Validation signals |
