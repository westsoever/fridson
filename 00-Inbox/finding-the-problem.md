# Finding the Problem

**Meeting recorded:** Saturday, June 27, 2026
**TLDR:** Office lifecycle management, predictive sensor maintenance, two-day demo development

---

## Executive Summary

- The team is focusing on **LifeCycle Management** for office buildings, aiming to transition from reactive to predictive maintenance using AI and sensor data.
- Several use cases were discussed including hygiene monitoring (cleanliness of tables), office hardware (printers/projectors), and infrastructure (plumbing/energy).
- A key technical goal is to connect a high-risk asset to a dashboard that triggers an automated alert (e.g., via Slack) to the relevant service team.
- The project scope is being narrowed to a demo-able version that can be built in two days, likely focusing on a single sensor use case.

---

## Problem Space

The group agreed to focus on **office building servicing and replenishment** (cups, paper, water). The "LifeCycle" was defined in three stages:

1. **Design/Build** - not the focus
2. **Operating** - all operations during the building's lifetime
3. **Predictive Maintenance** - knowing what's going to happen before it does

> "The problem we're solving is life cycle. It costs a lot of money... no matter how well you treat your office, it's gonna wear down."

The platform focus: somewhere between **Operating** and **Predictive** - the building already exists, and we want to know what will happen to it in the future.

---

## Potential Use Cases

| Use Case | Notes |
|---|---|
| **Hygiene** | Multimodal LLM analyzes photos/video of tables to detect if they need cleaning. Pings cafeteria to clean. Easy to demo. |
| **Office Hardware** | Monitoring printers and projectors. Needs more data than AI alone. |
| **Plumbing / Predictive** | Vibration or ultrasonic flow sensors to predict failures before they happen. |
| **Space Utilization** | Analyzing occupancy to optimize floor plans and reduce wasted space. |
| **Energy** | Integrating building data to automate climate control and reduce consumption. |
| **Gardening/Plants** | Dismissed - aesthetic, not a critical operational pain point. Scales better for greenhouses. |

---

## Decisions

- **Decision:** Focus the project scope on **office buildings and life cycle management** [by lennert]
- **Decision:** The demo must be achievable within a **two-day timeframe**
- **Decision:** Narrow down to **one specific sensor** and **one specific use case** (e.g., vibration sensor for a pump)

---

## Action Items

- [ ] Research existing life cycle maintenance software for inspiration and factual pitch data
- [ ] Upgrade to Pro plan for Cursor to facilitate team usage
- [ ] Narrow down to one sensor + one use case (e.g., vibration sensor for pump pressure)
- [ ] Build a basic HTML dashboard to visualize asset alerts

---

## Risks / Open Questions

- **Risk:** Training vision models for broken hardware/windows may be too complex for a short demo
- **Open Question:** What specific pressure or vibration threshold indicates a future leak?
- **Open Question:** Which sensor is most feasible for a two-day prototype - flow, pressure, or vibration?
