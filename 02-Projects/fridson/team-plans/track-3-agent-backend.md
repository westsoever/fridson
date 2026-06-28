# Track 3 — Agent Backend (the WOW)

**Owner:** Alex · **Mission:** Build the **AI property manager loop** — from a report, select the right contractors, send real RFQ emails, parse bids, negotiate one round, book a slot, and gate it behind PM approval. Emit a clean event for every step so Track 2 can show it. "80% quality" is explicitly fine — **real where stable, scripted fallback where not.**

> Read [[INTERFACES]] §3 (providers), §4 (events you emit), §5 (approve API). See [[RESOLUTION-AGENT]] for the detailed spec.

> ✅ **SHIPPED + PUSHED 2026-06-27** (`403ee22` → `origin/main` `4e36b43`). Self-contained Deno edge function `supabase/functions/agent/**` runs the whole loop — select → RFQ → bids → negotiate → book → PM approve — emitting all §4 events; §5 decision API implemented; 10 Deno tests pass. **Runs on Supabase Edge — Azure NOT needed.** Wired: `submitReport` now invokes it async (202).
>
> ⚠️ **Merge note:** main now also carries Alex's `ai-agent-flow` — durable **DB webhook** agents (`process-triage`/`process-research` + `report_agent_webhooks` migration). Both paths fire on a report; **reconcile to one canonical trigger** (the durable webhook is more robust) before stage. **Remaining is manual:** `bunx supabase@latest functions deploy agent process-triage process-research` (needs access token); set `SUPABASE_SERVICE_ROLE_KEY` (+ optional `RESEND_API_KEY`/`AGENT_LIVE_EMAIL=1` for real email — else labelled stubs).

---

## You own
- The agent service (Supabase Edge — **Azure NOT needed**) + the `/agent` API
- Provider **selection logic**, email RFQ/parse, negotiation, booking, approve/disapprove, audit log
- Writing events to the shared feed channel per [[INTERFACES]] §4

## You must NOT touch
- DB schema (request columns from Track 1) · `/schematic` & `/projection` UI (Track 2) · deck (Track 4)

## Depends on
- Track 1: provider directory + report object (the GATE — don't start heavy build until #1 + directory are demo-able)
- Blockers: ~~**Azure credits**~~ (not needed) · **demo vendor inboxes** optional (coordinate with Track 4 for controlled inbox if using real Resend email)

---

## Tasks (P3 #4–#7)
- [x] Scaffold the agent service + **provider selection** against [[INTERFACES]] §3 (mock dir, auto-swaps to Track 1's live `providers`) ✅
- [x] **Select ~3 of 50** providers by `trade` + `zone`; emit `providers.selected` with a human-readable `reason` ✅
- [x] RFQ emails + parse replies into comparable bids → emit `rfq.sent` + `bid.received` ✅ (real with creds; labelled stubs otherwise)
- [x] **Negotiate** one round within FM-set target/ceiling → emit `negotiation.round` ✅ (voice call = still stretch)
- [x] **Book a repair slot** → emit `slot.booked` "Technician booked for {date}" ✅
- [x] **PM approve/disapprove** API (§5) gates the booking — no autonomous spend — + **audit log** ✅
- [x] Prepare **recorded/seed fallbacks** (5 canonical demo reports, fixture bids, simulated booking) ✅

## Acceptance
- [ ] From one report, the feed shows: selected → RFQs sent → bids in → negotiated price → slot booked
- [ ] ≥1 **real** email sent to a controlled inbox + ≥1 **real** reply parsed (rest may be labelled pre-fetch)
- [ ] Approve confirms booking; Disapprove loops back to selection; full audit log visible
- [ ] Agent runs **async** — never blocks the scan success screen

## Guards
- No real purchases/payments. AI must disclose itself on any call. Label pre-fetched data as such in rehearsal notes. Emit at least the bold-path events even in fallback mode.
