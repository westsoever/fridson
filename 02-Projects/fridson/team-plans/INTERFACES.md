# INTERFACES — the shared contract

This is the **only surface shared between tracks**. Agree on it early; then everyone builds in parallel against these shapes instead of each other's code. If a shape must change, post in the team chat and update this file — don't silently diverge.

---

## 1. The report object (owned by Track 1)

The spine. Created on every scan→tap. Everyone reads it; only Track 1 changes its schema.

```json
{
  "id": "rep_001",
  "asset_id": "printer-3f",
  "asset_label": "Printer — 3rd floor",
  "zone": "3F",
  "location": { "floor": 3, "x": 0.62, "y": 0.31 },
  "issue": "out-of-paper",
  "route": "in-house",            // "in-house" | "contractor"
  "status": "open",               // open | routing | bidding | booked | approved | closed
  "created_at": "2026-06-28T14:00:00Z"
}
```

## 2. Asset + schematic coords (owned by Track 1, rendered by Track 2)

- One floorplan image per building (seeded).
- Each of the 5 assets carries `location: { floor, x, y }` where `x,y` are **0–1 fractions** of the floorplan image (resolution-independent). Track 2 multiplies by rendered width/height to place the marker.

## 3. Provider directory (owned by Track 1, queried by Track 3)

```json
{ "id": "prov_017", "name": "AquaFix ApS", "trade": "plumbing",
  "zone": "2F", "email": "aquafix@demo.test", "rate_eur": 85 }
```
~50 rows. Track 3 filters by `trade` (derived from issue) + `zone`.

---

## 4. Event feed (the Track 2 ↔ Track 3 bridge)

Track 3 **emits** these; Track 2 **renders** each as a step card in the projection. Track 2 builds against a mock emitter first; flipping to real is just pointing at the live channel (websocket/poll on the `events` table).

| Event | Emitted when | Payload (key fields) | Projection shows |
|-------|--------------|----------------------|------------------|
| `report.created` | scan→tap | `report_id, asset_id, zone, issue` | "New report: {issue} @ {asset}" |
| `location.pinpointed` | report saved | `report_id, location` | marker pulses on schematic |
| `providers.selected` | agent picks 3 | `report_id, selected[], reason` | "Selected 3 of 50 — {reason}" |
| `rfq.sent` | emails out | `report_id, count` | "RFQs sent to {count} providers" |
| `bid.received` | reply parsed | `report_id, provider, price_eur` | bid row added |
| `negotiation.round` | counter sent/recv | `report_id, provider, price_eur` | "Negotiated → €{price}" |
| `slot.booked` | slot held | `report_id, provider, date` | "Technician booked {date}" |
| `pm.decision` | PM approves/denies | `report_id, decision` | green ✓ / re-loop |

**Contract:** every event carries `report_id` + `ts`. Order on screen = by `ts`. Track 2 must tolerate missing events (render what arrives); Track 3 must emit at least the bold-path subset even in scripted-fallback mode.

---

## 5. Approve control (Track 3 API, surfaced by Track 2/admin)

- `POST /agent/decision { report_id, decision: "approve" | "disapprove" }`
- `approve` → emits `slot.booked` confirm + sets report `status=approved`.
- `disapprove` → re-runs `providers.selected`. **No autonomous spend** — booking is a hold until approved.

---

## Change log
| Date | Change |
|------|--------|
| 2026-06-27 | Contract drafted from [[ACTIVE_PLAN]] + [[INTERFACES]] split |
