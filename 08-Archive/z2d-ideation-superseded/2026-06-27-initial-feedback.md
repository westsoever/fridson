# Initial Feedback - Meeting Notes
**Date:** 2026-06-27  
**TLDR:** Agentic facility management, automated contractor negotiation, adoption barrier research

---

## Core Concept

The system sits between a detected facility problem and the person/contractor who solves it - bypassing traditional inventory management layers entirely. The key insight: go straight from problem detection to resolution.

## Product Flow

1. **Detection** - A camera scans a room. When the door closes, the system prompts: is anything broken? Is the table disorganized? This auto-generates a maintenance ticket.
2. **QR fallback** - Simpler entry point: scan a QR code in a space to report an issue or trigger a reorder.
3. **AI agent negotiation** - Once a ticket is created, an AI agent (via Twilio calls or SMS) contacts contractors to get bids, check availability, and negotiate within time/cost constraints.
4. **Approval workflow** - Results surface to a facilities/services manager. Under a threshold (e.g. €100/month) it auto-approves; above that, manual sign-off is required.

## Demo Direction (2PM)

Encapsulate the full vision in one end-to-end demo. Suggested scenario: **coffee runs out** - someone scans a code, system recognizes the issue, AI agent calls a supplier to arrange a new order and negotiate. Shows detection → ticket → negotiation → resolution in one loop.

## Open Questions / Next Steps

- **Why isn't it everywhere yet?** Need deep research into adoption barriers - is it a pricing problem, a trust problem, a sensor/infrastructure problem, or something else?
- The camera-based detection is ambitious (needs physical sensors). QR codes are the simpler, provable-first path.
- Twilio integration for agent calling/SMS is a strong differentiator - it makes the "AI as negotiator" angle tangible and demo-able.
- Distinguish between what needs AI (negotiation, judgment calls) vs. what is just automation (auto-reorder when fridge is empty).

## Key Insight from Discussion

> "If you're managing a huge building, the cost will be supplied - but if it's a fever-level urgent fix, find me someone who can do it."

The value prop scales with building/portfolio size. The bigger the operation, the more time saved on supplier calls, the more the agent pays for itself.
