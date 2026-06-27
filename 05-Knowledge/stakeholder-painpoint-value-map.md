# Fridson Stakeholder Pain Point & Value Map

Created: 2026-06-27

## Context

Fridson is currently framed as an office lifecycle / facility reporting and maintenance intelligence product. The repo positions the product around a practical demo wedge: **Scan → Tap → Route**. A building user scans a QR code on an asset or room, taps the issue, and the system routes the report to the right in-house facility manager or external contractor. The roadmap expands this into **Resolve** through sourcing/replacement support and eventually **Predict** through sensors and history-based failure prediction.

Core product layers:

1. **Capture** — QR scan and one-tap issue reporting.
2. **Route** — smart routing to the correct responder.
3. **Resolve** — sourcing brief, vendor outreach, quote comparison, and human-approved replacement workflow.
4. **Predict** — sensor data and maintenance history to identify failures before they happen.

## Stakeholder pain points and value resolution

| Stakeholder | Two-word pain point | What this means | How Fridson resolves it | Value created / measurable outcome |
|---|---|---|---|---|
| **Building owner / landlord** | **Hidden deterioration** | Asset problems accumulate quietly until they become expensive repairs, tenant complaints, or value erosion. | Converts scattered issue signals into maintenance history, recurring-problem analytics, and eventually predictive asset insights. | Higher asset protection, fewer surprise capex events, better documentation, stronger tenant retention. |
| **Asset manager / investor** | **Performance opacity** | It is hard to see which buildings, zones, assets, or vendors are driving cost, downtime, and risk. | Aggregates reports, routes, response patterns, and asset history into a clearer operating-performance layer. | Better NOI visibility, lower operating waste, improved investment reporting, more evidence for capex decisions. |
| **Facility manager / property manager** | **Triage overload** | Issues arrive through email, Slack, hallway comments, WhatsApp, phone calls, and vague complaints. | QR-based structured intake captures asset, location, issue type, and route automatically. | Less admin time, faster dispatch, fewer missed issues, fewer manual follow-ups. |
| **Tenants / occupiers** | **Service friction** | Tenants care about fast fixes but often do not know who to contact or whether anything will happen. | No-login QR reporting makes issue submission immediate and location-aware. | Better tenant experience, fewer repeated complaints, higher perceived service quality. |
| **Building users / employees / residents** | **Reporting hassle** | People notice issues but avoid reporting them if it requires forms, apps, logins, or writing explanations. | Scan the QR code, tap one issue, and get a confirmation that it has been sent. | Higher reporting rate, faster issue discovery, better comfort and safety. |
| **Visitors / guests** | **Navigation uncertainty** | Visitors need clean, safe, functional spaces but usually have no channel to report problems. | Simple QR reporting works without account creation and can be placed in high-traffic areas. | Better guest experience, more inclusive issue capture, less reputational damage from visible problems. |
| **Maintenance team / technicians** | **Context missing** | Technicians often receive vague tasks without exact asset, location, issue type, or urgency. | Report payload includes asset ID, zone, issue label, route, and optional history/photos in future versions. | Shorter diagnosis time, fewer wrong trips, higher first-time-fix rate. |
| **External vendors / contractors** | **Bad handoffs** | Contractors receive incomplete or misrouted requests, delaying service and creating back-and-forth. | Smart route sends contractor-relevant issues directly with location and context. | Faster acceptance, fewer clarification messages, better SLA performance. |
| **Cleaning / hygiene teams** | **Reactive cleaning** | Cleaning needs are discovered through complaints instead of real-time signals from rooms and users. | Issue buttons for spills, dirty rooms, no soap, or cleaning needs route directly to the right team. | Faster cleaning response, better hygiene quality, fewer visible service failures. |
| **IT / office hardware support** | **Device downtime** | Printers, projectors, and meeting-room equipment fail during work, meetings, or events. | Asset-specific QR pages for printers and meeting rooms route relevant device issues to support. | Less downtime, faster meeting recovery, fewer productivity interruptions. |
| **Security teams / emergency services** | **Incident ambiguity** | Safety and access incidents can be unclear, underreported, or routed through the wrong channel. | Structured reporting can separate safety/security categories and preserve an audit trail. | Faster escalation, clearer incident records, improved emergency readiness. |
| **Compliance / safety inspectors** | **Proof gaps** | Compliance depends on evidence that issues were noticed, routed, handled, and documented. | Creates timestamped records of reports, routes, and resolution status. | Stronger audit trail, lower compliance risk, easier inspection preparation. |
| **Municipality / regulators** | **Compliance uncertainty** | Regulators need confidence that building-code, accessibility, environmental, and safety obligations are met. | Long-term system records can document recurring issues, response times, and corrective actions. | Reduced regulatory risk, more transparent building operations. |
| **Insurance providers** | **Risk evidence** | Insurers need proof that risks are monitored, mitigated, and not ignored. | Maintenance logs, incident records, and predictive alerts make risk management visible. | Better claims documentation, potentially lower risk profile, fewer preventable incidents. |
| **Energy / ESG managers** | **Waste invisibility** | Energy leaks, comfort complaints, and inefficient equipment are hard to connect to daily operations. | Reports and future sensor feeds can identify patterns around HVAC, temperature, occupancy, and equipment failures. | Lower energy waste, better ESG reporting, more targeted efficiency improvements. |
| **Neighbors / local community** | **External disruption** | Noise, leaks, traffic, or building defects can affect people outside the property. | Better internal reporting and routing reduces unresolved problems that spill into the local environment. | Fewer complaints, better community reputation, lower escalation risk. |

## Priority interpretation

### Tier 1 — Sell and design for first

| Stakeholder | Why they are highest priority | Best Fridson promise |
|---|---|---|
| **Facility manager / property manager** | Owns the operational pain daily and benefits immediately from less triage. | “Every building issue arrives structured and routed.” |
| **Tenants / occupiers** | Their satisfaction affects retention, complaints, and perceived building quality. | “Anyone can report a problem in seconds.” |
| **Maintenance teams / vendors** | They determine whether issues actually get resolved. | “Every task comes with location and context.” |
| **Owner / asset manager** | They care about the economic upside: cost, risk, asset value, and documentation. | “Turn facility noise into asset intelligence.” |

### Tier 2 — Build credibility through operational outcomes

| Stakeholder | Why they matter | Fridson value angle |
|---|---|---|
| **Building users** | They are the largest signal source. | Increase issue capture through zero-friction reporting. |
| **Cleaning / hygiene teams** | They are a clear demoable routing path. | Convert hygiene complaints into immediate service tasks. |
| **IT / office support** | Printers/projectors are relatable and demo-friendly. | Reduce device downtime through asset-specific reporting. |
| **ESG / energy managers** | Future roadmap value. | Use reports and sensor patterns to reveal waste. |

### Tier 3 — Prove through records, auditability, and risk reduction

| Stakeholder | Why they matter | Fridson value angle |
|---|---|---|
| **Inspectors / regulators** | They create high consequence if requirements are missed. | Preserve an operational audit trail. |
| **Insurance providers** | They care about risk evidence. | Document risk reduction and incident handling. |
| **Security / emergency teams** | Less frequent but high-severity use cases. | Route urgent issues and preserve incident context. |

## Most pitchable two-word pain points

If the pitch needs to be short, use these four:

| Stakeholder | Pain point | Fridson line |
|---|---|---|
| **Occupants** | **Reporting hassle** | “Scan, tap, done.” |
| **Facility managers** | **Triage overload** | “Structured issues go to the right person automatically.” |
| **Technicians / vendors** | **Context missing** | “Every task includes asset, location, and issue context.” |
| **Owners / asset managers** | **Hidden deterioration** | “Every issue becomes asset intelligence.” |

## Strategic takeaway

Fridson should position itself as the **front door of building operations**: the simplest possible way for anyone to report an issue, plus the intelligence layer that turns reports into routed tasks, resolved work, and eventually predictive maintenance.

The sharpest message is not “facility management software.” It is:

> **From building complaint to resolved action — instantly routed, fully documented, and increasingly predictive.**

## Source basis

- Repository `README.md`: project is a Knowledge OS and stores consolidated frameworks in `05-Knowledge/`.
- `CRITICAL_FACTS.md`: Team Fridson is building an office lifecycle / predictive maintenance platform for Z2D Cohort #3.
- `06-Wiki/Problem.md`: core pain is reactive operations, no forward visibility, lifecycle cost, and manual coordination.
- `02-Projects/fridson/MVP-FLOW.md`: core demo is Scan → Tap → Route using QR-based reporting and Slack routing.
- `02-Projects/fridson/RESOLUTION-AGENT.md`: roadmap extends from reporting into sourcing, vendor outreach, negotiation, and human-approved resolution.
- Existing chat context: earlier stakeholder priority map grouped owners, asset managers, facility managers, tenants, users, technicians, vendors, compliance, insurance, ESG, security, regulators, visitors, and neighbors by value and interest.
