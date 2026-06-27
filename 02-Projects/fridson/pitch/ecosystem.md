# Ecosystem & Context — Minute 2

**Owner:** Track 4 (Pitch) · **Status:** Locked for Sun demo
**Anchors:** [[ACTIVE_PLAN]] Phase 5 · [[06-Wiki/decisions/2026-06-27-final-commitment]] (Minute 2) · [[05-Knowledge/stakeholder-painpoint-value-map]]
**Spoken in:** `script.md` → Minute 2.

> **The Minute-2 idea:** Reporting a hassle creates **context** — a timestamped, structured record of *what failed, where, when, and how it was resolved*. That same record is valuable to stakeholders beyond the property manager. One scan → many lenses.

---

## The core move

The tenant's 3-second scan produces **one structured event** (asset · location · issue · route · timestamp · resolution + audit trail). Fridson already has to create this record to route and resolve the issue — so the context is a **free by-product**, not extra work. Minute 2 shows that the *same event* lights up value for three secondary stakeholders.

> On stage this is **framing + a mock context record**, not real integrations (per Phase 5 anti-pattern guard). Show one ticket page with ≥2 stakeholder lenses on the same event.

---

## Secondary stakeholders (one concrete example each)

### 1. Insurer — **proof-of-issue**
Insurers need evidence that risks were noticed, mitigated, and not ignored.[^stakeholder]

> **Concrete example:** The 2nd-floor bathroom leak (`bathroom-2f`) is scanned at 14:32, auto-routed to a plumber, and a repair slot is booked the same afternoon — all timestamped with an audit trail. When a water-damage claim is filed, Fridson hands the insurer a **dated proof-of-issue + response record**: "detected 14:32, contractor dispatched 14:41, fixed same day." Faster claims, lower disputed liability, evidence the building mitigated promptly.

### 2. Energy / utility — **consumption & repair audit**
Energy leaks and inefficient equipment are hard to tie back to daily operations.[^stakeholder]

> **Concrete example:** The basement pump (`pump-basement`) is reported with "unusual noise." That repair event becomes a line in a **consumption & repair audit** — a failing pump running inefficiently is an energy cost. The same structured stream of equipment events feeds an energy/ESG view of which assets are driving waste, without a separate metering project.

### 3. Repair / compliance — **audit trail**
Compliance depends on provable records that issues were noticed, routed, handled, and documented.[^stakeholder]

> **Concrete example:** Every ticket carries a timestamped log — reported → routed → bids → negotiated → approved → booked → resolved. For a safety inspection, the property manager exports the **compliance audit trail** for an asset in one click, instead of reconstructing it from emails and memory.

---

## The same event, three lenses (mock context record)

| Lens | Sees | Value |
|---|---|---|
| **Property manager** (primary) | asset · location · issue · route · cost · approval | Less triage, faster resolution |
| **Insurer** | detection time · response time · resolution proof | Proof-of-issue for claims; lower risk profile |
| **Energy / utility** | asset type · failure mode · repair history | Consumption/repair audit; waste signals |
| **Repair / compliance** | full timestamped chain + sign-off | Audit trail; inspection-ready records |

*Demo artifact: one ticket page (e.g. the bathroom leak) toggling between the PM lens and the Insurer/Compliance lens on the same event.*

---

## The triage-shift line (≤20s — spoken verbatim)

> **"Before Fridson, the property manager *was* the system — they triaged every vague report, picked up the phone, chased three contractors for quotes, and haggled on price. Now? They get one notification with a negotiated recommendation, and they do one thing: approve, or disapprove. The orchestration runs itself."**

*(~18s at pitch pace. This is the hinge of Minute 2: PM orchestrated everything → now they just approve.)*

---

## Sources

[^stakeholder]: [[05-Knowledge/stakeholder-painpoint-value-map]] — Insurance providers ("Risk evidence"), Energy/ESG managers ("Waste invisibility"), Compliance/safety inspectors ("Proof gaps"), each mapped to the structured-record by-product.
