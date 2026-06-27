# Data Brain - Meeting Notes
**Date:** 2026-06-27  
**Project:** Fridson (Z2D Hackathon)

---

## Core Concept

**"24/7 AI Property Manager"** - the hero positioning for the product.

An AI suite that handles everything end-to-end for office space property management, including:
- Supply & inventory management
- People management
- Reporting (automated, AI-generated)
- Hazard identification (fire escapes, safety systems)
- Issue detection and flagging

---

## Key Discussions

### Automated Inventory Sync
Idea surfaced to auto-update inventory based on purchase invoices from the office/procurement department. Every time a purchase is made, the inventory updates automatically - flagged as potentially high-value for clients vs. manual inventory tracking.

### Stakeholder-Facing AI Agent (Open API)
Any stakeholder that has any stake in the state/health of the property can use the AI agent to ask it questions directly. This is a core product principle.

**Who this includes:**
- Building managers
- Employees in the building
- Janitors (e.g. "schedule things" -> just ask the agent instead)
- External parties like energy providers

**Example queries:**
- "How is the energy level of this building?"
- "What is the status of the fire escape system?"
- Energy providers can query billing and consumption data via a somewhat open API

This positions the AI agent as a universal interface into the property's health - not just an internal tool, but an externally queryable knowledge layer exposed through a controlled API.

### Demo / Feedback Strategy
- Approach: present the full scope of features to clients tonight
- Let client feedback dictate what to cut ("throw everything at them, and they'll tell us what they don't like")
- Risk to manage: avoid feedback of "you're doing too much" - need to frame scope deliberately
- Plan to build a mock-up / demo using ChatGPT or similar tool

### Branding & Hero Copy
Debate around what the product actually is called / positioned:
- "Property" feels like real estate to end-users
- "Office" is more specific but potentially too niche
- "SaaS-sounding" language to avoid
- Leading candidate: **"24/7 AI property manager for office spaces"**
- Full scope pitch: from supply to people management to reporting, hazards, fire escapes, compliance

### Website / Landing Page
- Hero line direction: "24/7 AI property manager - does everything for you"
- Scope on the landing: supplying, people management, reporting, hazard/fire escape compliance
- Draft being prepared for review before posting; Danish version also planned

---

## Action Items
- [ ] Finalize and review website copy draft before posting
- [ ] Post Danish version of the website copy
- [ ] Build demo/mock-up (ChatGPT or equivalent) for client feedback session
- [ ] Gather client feedback this evening - use it to narrow product scope
- [ ] Define API access model for external stakeholders (energy providers etc.)
