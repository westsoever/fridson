# Track 1 — Capture & Data Foundation

**Owner:** Chris
**Mission:** Own the **data spine** everyone else builds on — verify the scan→tap capture, lock the report shape, and seed the floorplan coords + 50-provider directory. **Ship the contract first; the team is blocked until you do.**

> Read [[INTERFACES]] sections 1–3. Those shapes are *your* deliverable.

> ✅ **SHIPPED + PUSHED 2026-06-27** (`403ee22`, now on `origin/main` → `4e36b43`). Data spine built: 4 migrations (asset coords · full report record + trigger · 55-row provider directory · events feed + realtime), `floorplan.svg` + coord map, DB types. Deviations logged in [[INTERFACES]]. **Remaining is manual:** apply migrations to Supabase — via Lovable's Supabase sync or `bunx supabase@latest db push` (needs access token + DB password). See [[ACTIVE_PLAN#Blockers]].

---

## You own
- Supabase tables + seed data: `reports`, `assets` (with coords), `providers`
- The Capture pages `/r/{asset}` (verify only — **don't rebuild**, it works)
- The admin/reports page (verify the persisted row shows)

## You must NOT touch
- `/schematic`, `/projection` (Track 2) · `/agent` + agent service (Track 3) · deck/`pitch/` (Track 4)

## Provides → others
- **Track 2:** asset `location {floor,x,y}` coords + floorplan image
- **Track 3:** the provider directory to query + the report object to act on

---

## Tasks (your slice of P1 + Roadmap #3)
- [x] Verify scan→tap on a **phone** for all **5 assets**; two distinct routes (printer/out-of-paper → in-house "Sent to facility team"; bathroom/leak → contractor "Sent to contractor") ✅
- [x] Confirm each report persists the full record per [[INTERFACES]] §1: `asset · zone · location · issue · route · status · timestamp` ✅
- [x] Confirm the **admin/reports page** shows the new row < 2s (this is the live-demo backup) ✅
- [x] Add `location {floor,x,y}` (0–1 fractions) to each of the 5 seed assets ✅
- [x] Seed **one floorplan image** (`public/floorplan.svg`) for the demo building + coord map for Track 2 ✅
- [x] Seed the **provider directory** (55 rows: name, trade, zone, email `*@demo.test`, rate) ✅

## Acceptance
- [ ] All 5 `/r/{asset}` load < 2s on 4G, correct asset + zone
- [ ] A tapped issue → a row in admin within 2s, two issues → two visibly different destinations
- [ ] `assets` + `providers` tables populated and queryable; coords map onto the floorplan

## Guards
- No login, no typing, keep the success screen instant. Don't extend schema without telling the team (update [[INTERFACES]] change log). Email field must be **demo/sandbox**, never real vendors.
