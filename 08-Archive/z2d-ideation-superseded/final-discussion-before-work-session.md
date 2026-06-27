# Final Discussion Before Work Session

**Date:** 2026-06-27  
**Type:** Strategy / Pre-build alignment

---

## Core Concept

Fridson is a suite of AI agents for property management. The central idea:
> One system connects all stakeholders, fixes each one's pain points, and makes those pain points interconnected - fixing one helps the others.

---

## The Flow (as discussed)

```
Human scans asset (QR / RFID / form / agent chat)
        |
        v
   Fridson (data pool)
        |
   +---------+----------+
   |         |          |
   v         v          v
Context   Report    Audit/PO
(tech)  (property  (insurer /
         manager)  compliance)
```

1. **Step 1 - Report:** Human scans the problem and is done. Agent takes over.
2. **Step 2 - Context:** Fridson auto-fills asset, location, and issue for the technician/service provider.
3. **Step 3 - Report & Purchase Order:** Once resolved, the record feeds back into Fridson for audit, insurance, and compliance use.

Note: a **circular diagram** was suggested to visualize this loop visually.

---

## Stakeholders & Pain Points

| Stakeholder | Pain Point | How Fridson Solves It |
|---|---|---|
| **Occupant / Reporter** | Reporting is painful and slow | QR/RFID scan or agent chat; job done in one step |
| **Technicians** | Lack of context on what/where/why | Agent auto-generates asset + location + issue brief |
| **Service Providers** | Same as technicians (coffee, printers, consumables, etc.) | Same context pipeline |
| **Property / Facility Manager** | Does all triaging and coordination manually | Now only approves/rejects; AI handles routing |
| **Safety & Compliance** | Needs insurance proof and audit trail | System auto-generates reports from issue data |
| **Energy & Utilities** | Costly repairs, hard to audit, need predictive analytics | Predictive analytics from historical asset data |

---

## The Three AI Agents

### 1. AI Property Manager
- Collects incoming issues (from scan, form, or chat)
- Analyzes and routes intelligently to the right technician or service provider
- Acts as a bridge between the issue and the workforce
- Replaces manual triaging by the property/facility manager

### 2. AI Technician / Service Provider Agent
- Receives full context: asset, location, issue
- Improves technician/provider workflow efficiency
- Eventually feeds outcomes back into the data pool

### 3. AI Compliance Agent
- Handles audit reporting for insurers
- Generates proof-of-issue documentation (e.g. broken asset was not human error)
- Supports energy & utility cost audits
- Surfaces predictive analytics for costly repairs

> Note: these three agents could be framed as sub-agents under one unified Fridson AI property manager umbrella.

---

## Key Design Decisions

- **Data pool first:** Everything that happens in the system is fed into a central data pool. This powers context for technicians, reports for managers, and audits for insurers - all from the same source.
- **No manual handoffs:** The property manager's role shifts from doing to approving. The AI handles the rest.
- **Interconnected value:** The same event (e.g. a broken roof) generates value across multiple stakeholders - the technician gets context, the manager gets a routed ticket, the insurer gets a report.

---

## Demo Strategy Notes

- Keep the demo to **~2-3 minutes** - show what we do, let questions drive elaboration
- Lead with: *"We're building Fridson - a suite of AI employees for property management"*
- Show the 3 agents clearly, don't over-explain the interconnections upfront
- The diagram (circular flow) should make the system click visually

---

## Raw Notes (from screen)

- We need a circular diagram
- Human reports to Fridson → Fridson writes report and initializes ticket for landlord
- AI Property: collecting issues, analyses and routes intelligently to the right technician or service provider (acts as a bridge)
