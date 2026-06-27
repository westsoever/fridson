# Track 3 — Agent Backend (the WOW)

**Owner:** Alex · **Mission:** Build the **AI property manager loop** — from a report, select the right contractors, send real RFQ emails, parse bids, negotiate one round, book a slot, and gate it behind PM approval. Emit a clean event for every step so Track 2 can show it. "80% quality" is explicitly fine — **real where stable, scripted fallback where not.**

> Read [[INTERFACES]] §3 (providers), §4 (events you emit), §5 (approve API). See [[RESOLUTION-AGENT]] for the detailed spec.

---

## You own
- The agent service (host on **Azure** — see blocker) + the `/agent` API
- Provider **selection logic**, email RFQ/parse, negotiation, booking, approve/disapprove, audit log
- Writing events to the shared feed channel per [[INTERFACES]] §4

## You must NOT touch
- DB schema (request columns from Track 1) · `/schematic` & `/projection` UI (Track 2) · deck (Track 4)

## Depends on
- Track 1: provider directory + report object (the GATE — don't start heavy build until #1 + directory are demo-able)
- Blockers: **Azure credits**, **demo vendor inboxes** (coordinate with Track 4 to create 2–3 controlled inboxes)

---

## Tasks (P3 #4–#7)
- [ ] **Select ~3 of 50** providers by `trade` (from issue) + `zone`; emit `providers.selected` with a human-readable `reason`
- [ ] Send **real RFQ emails** to controlled inboxes; parse replies into comparable bids → emit `rfq.sent` + `bid.received`
- [ ] **Negotiate** one real email round within FM-set target/ceiling → emit `negotiation.round` (voice call = stretch only)
- [ ] **Book a repair slot** (calendar hold / confirmation) → emit `slot.booked` "Technician booked for {date}"
- [ ] **PM approve/disapprove** API (§5) gates the booking — no autonomous spend — + an **audit log** of every step
- [ ] Prepare **recorded/seed fallbacks** (pre-fetched bids, pre-sent email, pre-booked slot) so it never breaks live

## Acceptance
- [ ] From one report, the feed shows: selected → RFQs sent → bids in → negotiated price → slot booked
- [ ] ≥1 **real** email sent to a controlled inbox + ≥1 **real** reply parsed (rest may be labelled pre-fetch)
- [ ] Approve confirms booking; Disapprove loops back to selection; full audit log visible
- [ ] Agent runs **async** — never blocks the scan success screen

## Guards
- No real purchases/payments. AI must disclose itself on any call. Label pre-fetched data as such in rehearsal notes. Emit at least the bold-path events even in fallback mode.
