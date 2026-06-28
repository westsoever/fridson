# Dry-Run Checklist — T-10 + Fallback Queue

**Owner:** Track 4 (Pitch) · **Gate:** Full-team dry-run before **Sun 16:00**
**Script:** [[pitch/script]] · **Logistics:** [[pitch/logistics]] · **QR props:** [[pitch/qr-codes]]

Run the **T-10 checklist** on stage, off the clock, immediately before the live demo or dry-run. Arm all fallbacks **before** T-10.

---

## Fallback recording queue (arm first)

Every live beat in Minute 1 needs a cued clip. Collect from Tracks 1–3; presenter confirms one keystroke to switch tabs.

| Priority | Recording | Covers | Owner track | Cued tab label | Status |
|----------|-----------|--------|-------------|----------------|--------|
| 1 | **Full 60s flow** | Scan → pinpoint → report → route → bids → negotiate → book → approve | All | `FALLBACK-FULL` | [ ] |
| 2 | Scan → success | Camera/QR failure | Track 1 | `FALLBACK-SCAN` | [ ] |
| 3 | Projection / activity feed | Feed stalls mid-demo | Track 2 | `FALLBACK-FEED` | [ ] |
| 4 | Agent steps | No bid / no email / agent error | Track 3 | `FALLBACK-AGENT` | [ ] |

**Presenter keystroke:** Confirm OS shortcut or manual tab switch to each fallback **without** looking away from the audience for more than 2 seconds. Rehearse once with fallbacks already playing at 0:00.

**Honesty rule:** If showing pre-fetched bids or a pre-booked slot, say so in rehearsal — label prepared data on admin/reports backup.

---

## T-10-minute checklist (on stage, off the clock)

Run in order. Do not start the timed 3:00 pitch until all boxes pass.

| # | Check | How to verify | Pass |
|---|-------|---------------|------|
| 1 | **Projection view open + reset** | Open `https://fridson.lovable.app/projection?feed=real` on the big screen; schematic legible from back of room; feed zeroed/idle | [ ] |
| 2 | **Phone on venue Wi-Fi** | Presenter phone unlocked, brightness max, notifications off, camera app open, same network as laptop/projector | [ ] |
| 3 | **5 QR codes on table** | All printed from [[pitch/qr-codes]]; **`meeting-4f` hero** within arm's reach; each scans from ~30 cm | [ ] |
| 4 | **Backup tab — workspace** | `https://fridson.lovable.app/workspace` (or admin/reports) open; shows persisted report if feed/Slack fails | [ ] |
| 5 | **Full-flow recording at 0:00** | `FALLBACK-FULL` tab cued; switch keystroke confirmed | [ ] |
| 6 | **Business-case slide ready** | Deck on Minute 3 slide; numbers memorized from [[pitch/business-case]] | [ ] |
| 7 | **Secondary fallbacks armed** | `FALLBACK-SCAN`, `FALLBACK-FEED`, `FALLBACK-AGENT` tabs open and tested | [ ] |
| 8 | **Scan-fallback bookmarks** | Phone bookmarks: all 5 `/r/{asset}` URLs (especially `/r/meeting-4f`) | [ ] |
| 9 | **Approve → RFQ email** | After hero scan: Approve in workspace → check `AGENT_MOCK_INBOX` for RFQ with report ID (or confirm `rfq.sent` in projection feed) | [ ] |

---

## Dry-run acceptance (after T-10)

From [[pitch/script]] — all must pass before **16:00** judging:

- [ ] End-to-end run hits **exactly 3:00** (re-time narration if over/under)
- [ ] Each minute maps to its source section (Min 1 live · Min 2 ecosystem · Min 3 business case)
- [ ] Every live beat has a **tested** fallback (simulate one failure per beat)
- [ ] Minute 3 business-case narration ≤ 60s

---

## Failure drill (optional 5 min)

Run once with the team watching:

1. **Scan fail** → open bookmark `/r/meeting-4f`, continue narrating.
2. **Feed stall** → switch to `FALLBACK-FEED`, say *"this is the same flow we just triggered."*
3. **Agent error** → switch to workspace/admin showing pre-fetched data; label honestly.
4. **Total failure** → play `FALLBACK-FULL` end-to-end; continue to Minutes 2–3 on slides.

---

## Human-action queue (remaining)

| When | Action | Who |
|------|--------|-----|
| Sun ~09:00 | Day 2 check-in on [Z2D Dashboard](https://z2d-base.lovable.app/dashboard) | Any team member with login |
| Before dry-run | Record + cue all 4 fallback clips | Tracks 1–3 |
| Sun **15:00** | Milestone 2 submit — use [[pitch/milestone-2-copy]] | Lennert or admin (Shuhia) |
| Before **16:00** | Full-team dry-run using this checklist | Whole team |
| **16:00** | Live demo & judging | Presenter + team |
