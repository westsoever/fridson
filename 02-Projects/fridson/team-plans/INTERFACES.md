# INTERFACES — the shared contract

This is the **only surface shared between tracks**. Agree on it early; then everyone builds in parallel against these shapes instead of each other's code. If a shape must change, post in the team chat and update this file — don't silently diverge.

> **Where these live in code:** the app is at `fridson-app/` (repo `westsoever/fridson-app`). Schema/seed → `fridson-app/supabase/`; pages & components → `fridson-app/src/`. The shapes below are the contract; the implementation is in those files.

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
| 2026-06-27 | **Track 1 locked the data layer.** Schema/seed shipped in `fridson-app/supabase/migrations/20260627190000–190300_track1_*.sql`. Deviations from the draft below — they reflect what the working app already implements. |

---

## Track 1 implementation notes (authoritative — what's actually in the DB)

**`reports`** — the row now carries the full §1 record (denormalized on insert by a DB trigger, so the capture page is unchanged):
`id, asset_id, asset_label, zone, location {floor,x,y}, issue, issue_label, route, status, ai_summary, ai_suggestion, ai_severity, ai_error, contractors, approved_at, researched_at, created_at`.
- **`route` values are `inhouse` | `external`** (NOT `in-house` | `contractor`). Mapping: `inhouse` = in-house FM, `external` = contractor. The whole app + Slack routing already use these.
- **`status` values are `awaiting_ai` | `awaiting_approval` | `approved` | `researching` | `done` | `failed`** (NOT `open|routing|bidding|booked|approved|closed`). These are the lifecycle states Track 3's agent actually drives. `approved` is common to both.
- **`issue`** is the §1 field name; it's a stored mirror of `issue_label` (the source of truth). Read either.
- `asset_label`, `zone`, `location` are copied from the asset at insert time (BEFORE INSERT trigger) so a report is self-contained — no join needed for Track 2 markers / Track 3 actions.

**`assets`** — added `location jsonb` = `{ floor, x, y }`, `x,y` are 0–1 fractions of `/floorplan.svg` (viewBox 800×1200, origin top-left), `floor` = storey (basement = 0). Seeded for all 5 assets. Coords also in `fridson-app/public/floorplan.coords.json`.

**Floorplan** — `fridson-app/public/floorplan.svg` (5 stacked floors 4F→B1). Served at `/floorplan.svg`. Track 2: multiply asset `x,y` by rendered w/h to place a marker.

**`providers`** — `{ id, name, trade, zone, email, rate_eur, created_at }`, 55 rows (≈50), all emails `*@demo.test`. Selectable via `?select=id,name,trade,zone,email,rate_eur` (matches Track 3's `fetchProviders`).
- `trade` ∈ `plumbing | hvac | electrical | appliance | av | cleaning | it | mechanical | general` (covers Track 3's full `Trade` set).
- `zone` ∈ floor code `B1|1F|2F|3F|4F` **or** `ALL` (city-wide). Suggested match: `provider.zone = 'ALL' OR provider.zone = split_part(asset.zone,'-',1)`. (Track 3's `floorOf` leaves `ALL` un-tokenised, so ALL vendors rank as out-of-floor fallback — intended.)
- issue→trade (matches Track 3's `tradeForIssue`): printer→`it`; bathroom→`plumbing` (or `cleaning`); pump→`mechanical` (or `plumbing` on leak); meeting_room→`av` (or `hvac` on too cold/hot); kitchen→`appliance` (or `cleaning` on spill); else→`general`.

**`events`** — `{ id, report_id (FK), type, payload jsonb, ts, created_at }`. RLS: public read + insert. Realtime enabled (`supabase_realtime` publication) on `events` + `reports`; poll `ORDER BY ts` is the fallback.
- **Track 1 auto-emits `report.created` + `location.pinpointed`** via DB trigger on report insert (they're inherent to report creation). **Track 3 emits the rest** (`providers.selected`, `rfq.sent`, `bid.received`, `negotiation.round`, `slot.booked`, `pm.decision`). `type` is free text (canonical list in the table comment) so Track 3 isn't blocked by an enum.
