# Final Commitment
**Date:** 2026-06-27  
**Meeting:** Final commitment - pitch structure alignment  
**TLDR:** Locking the Fritzson pitch structure, live scanning demo flow, and 3-minute presentation arc

---

## Core Definition (Source of Truth)

> **Fritzson is a suite of AI employees for property management.**

This is the agreed canonical description - superseding all previous iterations.

---

## How It Works (User Flow)

1. **Onboarding** - Property manager feeds the schematics of the building into Fritzson
2. **Tenant reports an issue** - Tenant opens the app, scans the problematic machine/asset
3. **Tap to confirm** - Tenant taps the problem type; no further action needed from their end
4. **Fritzson takes over** - Automatically creates a structured report including:
   - Asset identity
   - Location within the building
   - Nature of the issue
5. **Auto-routing** - Fritzson checks the contractor/technician/service provider list, selects relevant candidates (e.g. 3 out of 50)
6. **Negotiation** - Contacts them, gets bids, negotiates prices, and books a repair slot

The tenant never needs to contact anyone. The property manager only needs to approve or disapprove - the orchestration is fully automated.

---

## Demo Strategy (3-Minute Pitch Arc)

### Minute 1 - Live Demo + Running Commentary

- **~20 sec intro:** Set the scene - "It's always a hassle to report problems in your workplace. Coffee machine is broken. Printer is out of paper. What do you do?"
- **Scan the problem** (presenter does it live)
- **Background visual (projected behind presenter):**
  - Building schematic appears
  - AI agent pinpoints the exact location of the reported issue
  - Report is created in real time (asset, location, issue)
  - Contractor list is queried; relevant providers are selected
  - Emails sent, bids requested, negotiation begins - all visible in the background
- **Live narration** while it's happening: "Our agent is now looking for contractors, bidding for prices, sending emails..."
- Target: entire flow visible and explained within ~1 minute

### Minute 2 - Context & Ecosystem

- Reporting a hassle creates **context**
- Context can be consumed by **other stakeholders:**
  - Insurers
  - Energy utilities
  - Repair/compliance teams
- Introduce the **triage shift:** before Fritzson, the property manager had to orchestrate everything manually. With Fritzson, they simply approve or disapprove. The routing is automatic.

### Minute 3 - Business Case

- **Cost reduction** by X amount
- **Time improvement** (faster resolution cycles)
- **Quality improvement** across all parties
- Key framing: *"If we can reduce cost and do it way faster while achieving 80% of the quality - that is still a win."*

---

## Key Decisions Made

| Decision | Outcome |
|---|---|
| Canonical product description | "Suite of AI employees for property management" |
| Demo format | Live scan during pitch, background agent activity projected |
| Pitch length | 3 minutes total, 1 min per section |
| Quality tradeoff | 80% quality + lower cost + faster = acceptable and wins |
| Property manager role post-Fritzson | Approve / disapprove only (auto-routing handles the rest) |

---

## Action Items

- [ ] Build the live scanning demo so it works in real-time during the pitch
- [ ] Prepare the background projection (schematic + agent activity feed)
- [ ] Quantify the cost/time improvement claims for Minute 3
- [ ] Define the secondary stakeholder use cases (insurers, energy utilities) for Minute 2
- [ ] Confirm demo hardware setup (who presents, where the screen goes)
