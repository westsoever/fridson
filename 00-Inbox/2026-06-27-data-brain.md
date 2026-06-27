# Data Brain - Meeting Notes
**Date:** 2026-06-27  
**Project:** Fridson (Z2D Hackathon)

---

## Core Concept

**"24/7 AI Property Manager"** - the hero positioning for the product.

Fritzen.ai is an AI layer that sits above all physical data points of a building, allowing any stakeholder to query it through an AI agent. Think of it as a **digital twin** for office properties - all physical data extracted from a building goes into a database, and anyone can talk to it via AI.

An AI suite that handles everything end-to-end for office space property management:
- Supply & inventory management
- People management
- Reporting (automated, AI-generated)
- Hazard identification (fire escapes, safety systems)
- Issue detection and flagging
- Compliance (energy, security, structural)

---

## Key Discussions

### The Digital Twin Insight
The clearest articulation of the value proposition emerged mid-session: take all physical data points that can be extracted from a building, put them in a database, and let anybody talk to it with an AI agent. Fritzen.ai is not just a tool for one role - it's a universal interface into the property's health.

> "We take all the physical data points that you can extract from a building, put them in a database, and let anybody talk to it with an AI agent."

### Stakeholder Mapping
Extensive effort was spent identifying who actually has a stake in an office building. Key insight: each stakeholder has a distinct role, interest, and responsibility. The coordination mess between all of them is exactly the problem Fritzen solves.

| Stakeholder | Core Interest | Key Tasks / Concerns |
|---|---|---|
| Owner / Landlord | Asset value, rent collection | Collect rent, insurance, structural integrity, building schematics |
| Tenants / Occupants | Operational environment | The company renting the space |
| Building Users | Comfort & functionality | Employees, residents, visitors - want it clean and working |
| Facility Manager | Day-to-day operations | Supplies, maintenance scheduling, janitor-level tasks |
| Maintenance / Technicians | Physical systems | External contractors coming in to fix things |
| IT Workers | Data & connectivity | Care about the building's data infrastructure |
| Building Company | Construction & structure | Structural integrity |
| Service Regulators | Compliance | Energy, safety, fire regulations |

Key distinction: **tenants** = the company renting the space; **building users** = the people actually in it (employees, visitors, residents).

### Fritzen's Position in the Ecosystem
Fritzen.ai sits as a **unifying layer** between all stakeholders. Instead of all these groups needing to communicate with each other constantly (the coordination mess), they all talk to Fritzen, which references the same digital twin.

> "All of these different stakeholders - they can talk to Fritzen about their problems regardless of what those problems are."

The building company cares about construction. The office manager cares about supplies. The IT workers care about the data. They all need to talk to each other all the time - and that's where the mess is. Fritzen replaces that coordination layer.

### Pain Points Framework
The team converged on a structured approach to define what to build:
1. For each stakeholder, define their biggest pain points in ~2-word statements
2. Rank stakeholders by pain severity - biggest pain = biggest opportunity
3. Map what Fritzen can do for each (focus on "what we can do for them", not "what they do")
4. Identify overlapping solutions that serve 3-4 stakeholder types simultaneously

A ChatGPT-generated priority matrix (stakeholders organized by value/interest priority, with pain points) was used as a working document during the session.

### Stakeholder-Facing AI Agent (Open API)
Any stakeholder with a stake in the property's health can query the AI agent directly - not just internal staff. This is a core product principle.

**Who this includes:**
- Building managers, employees, janitors (e.g. skip scheduling tools - just ask the agent)
- External parties like energy providers

**Example queries:**
- "How is the energy level of this building?" (energy provider)
- "What is the status of the fire escape system?" (facility manager)
- Billing/consumption data queryable by energy providers via a somewhat open API

### Automated Inventory Sync
Inventory gets auto-updated based on purchase invoices from the office/procurement department. Every purchase = automatic inventory update. Flagged as high client value vs. manual tracking.

### Tech Stack Components to Combine
- QR codes (existing)
- Voice agents (existing)
- AI agent layer (Fritzen core)
- Goal: make something that works well for 3-4 stakeholder types as a demo

### Demo / Feedback Strategy
- Present full scope to client/stakeholders tonight
- Let feedback dictate what to cut ("throw everything at them, subtract from feedback")
- Risk: don't let the only feedback be "you're doing too much" - frame scope deliberately
- Build mock-up using ChatGPT or similar

### Branding & Hero Copy
- "Property" feels like residential real estate - avoid for B2B office context
- "Office" sounds niche / too SaaS-y
- Leading candidate: **"24/7 AI property manager for office spaces"**
- Full pitch scope: supply, people management, reporting, hazards, compliance

### Website / Landing Page
- Hero line: "24/7 AI property manager - does everything for you"
- Draft being reviewed before posting; Danish version also planned

### Scope: Office vs. Residential
Agreed to focus on **office buildings** for now. Large residential buildings (many occupants) could be a future market but are deliberately excluded from initial scope.

---

## Action Items
- [ ] Finalize and review website copy draft before posting
- [ ] Post Danish version of the website copy
- [ ] Build demo/mock-up (ChatGPT or equivalent) for client feedback session
- [ ] Gather client feedback this evening - use it to narrow product scope
- [ ] Define pain points per stakeholder (~2-word statements), ranked by severity
- [ ] Map what Fritzen can do for each stakeholder (not just what they do)
- [ ] Identify 3-4 stakeholder workflows where QR codes + voice agents + AI agent overlap
- [ ] Define API access model for external stakeholders (energy providers etc.)
- [ ] Reach out to Clara (after session work is done)
