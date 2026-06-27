# Pain Points Definition

**Date:** 2026-06-27
**Meeting:** PainPoints Definition — Z2D Hackathon (Fridson)
**TLDR:** Predictive maintenance transition, automated repair workflows, AI agent demo strategy

---

## Pain Points Identified

Five facility management pain points were reviewed. Two were flagged as the strongest fit for the product:

### 1. High Friction Reporting *(primary focus)*
Employees who notice problems have no easy way to report them. Email is effort — they stop reporting. This is a core problem the product solves via QR/RFID-based reporting.

### 2. Manual Coordination *(primary focus)*
Routing to the right person (in-house vs. contractor) happens over WhatsApp or email. No log, no SLA, no accountability.

### 3. No Forward Visibility
No signal tells the facility manager what will fail next week. Everything is identical until one thing breaks.

### 4. Reactive Operations
Teams fix things after they break. No proactive inspection catches issues early. The product aims to shift this to **predictive maintenance**.

### 5. Life Cycle Cost Accumulation
Deferred maintenance compounds. A pump that vibrates for weeks becomes a flood.

---

## Predictive Maintenance Discussion

The team discussed moving from reactive → predictive maintenance. Key ideas:

- **AI-generated maintenance reports** (monthly) — similar to consultancy output reports, but automated
- **Predictive modeling from technical reports** — the AI synthesises historical data to flag upcoming failures
- **Usage-correlated predictions** — example: printer page count correlates to cartridge depletion and printer lifespan. After ~10,000 pages → proactive replacement. Also useful for ordering cartridges monthly.
- **Priority filter:** Focus on use cases that are more damaging (financially or operationally) — printer cartridges were considered too trivial to impress stakeholders.

---

## Demo Strategy

**Agreed demo flow:**

1. Person scans a broken machine (QR code or photo)
2. The AI agent processes the report — back end visible on screen for ~10 seconds (agent working through the job)
3. **Low-cost issue** → automatically routed and resolved
4. **High-cost issue** → AI calls the reporter to gather more detail (what exactly is broken, etc.)
5. Agent then scans contractors and sends out bids

**Narrative script idea:**
- Reporter walks up to broken printer, tries kicking it — still broken
- Scans it → 1-2 min later receives an AI phone call asking follow-up questions
- One team member plays the role of the contractor receiving the job

**Key differentiation:**
- Low cost vs. high cost routing logic (differentiates automation depth)
- Live AI call during demo adds drama and believability

---

## Open Items / Next Steps

- Decide on the single sensor + use case for the 2-day demo (leading idea: vibration sensor on a pump)
- Build the demo flow: scan → AI processes → call or auto-route
- Facebook group post (Danish + English) after break — team photo needed
- Alex (product manager) to keep schedule updated

---

*Status: Raw capture — process into project files*
