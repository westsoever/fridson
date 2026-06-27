# Lovable Prompt + Validation Map

**Project:** Z2D Lifecycle Platform · Team Fridson  
**Source spec:** [[MVP-FLOW]]  
**Use:** Copy the prompt block below into Lovable. Use the validation map to verify the build before Pitch & Dine (Sat 20:00).

---

## Lovable prompt (copy from here)

```
Build a mobile-first web app called "Z2D Lifecycle" — a QR-based facility issue reporter for office buildings. No login required for reporters. Target: hackathon demo on a phone in under 90 seconds.

## Core user flow (3 steps)

1. SCAN — User scans a printed QR sticker. QR encodes URL: /r/{asset-id}
2. TAP — User sees asset context + a grid of large tap targets for common issues. One tap submits.
3. ROUTE — System sends a formatted message to the correct Slack channel (in-house FM vs external contractor).

## Pages

### 1. Asset report page — `/r/:assetId`
- Mobile-first, loads in < 2s on 4G
- No authentication
- Header: product name "Z2D Lifecycle" (small) + asset name (large, e.g. "Printer · 3rd floor East")
- Subheader: zone label (e.g. "3F-East") + asset type badge
- Optional placeholder image area for asset photo (use a generic icon per type if no image)
- Grid of 4 large tappable issue buttons (min 48px touch targets, full width on mobile, 2-column grid)
- Issue buttons vary by asset type (see seed data below)
- On tap: show loading spinner → success screen

### 2. Success screen (same route, post-submit state)
- Green checkmark
- Text: "Sent to facility team" (or "Sent to contractor" when routed externally)
- Summary: asset name + issue label
- "Report another issue" button resets to issue grid

### 3. Admin seed page — `/admin` (simple, no auth for MVP)
- Read-only table of all reports: timestamp, asset, issue, route (inhouse/external)
- Useful for demo backup if Slack fails
- Link from footer on report page (small "Admin" text link)

## Seed data — pre-load exactly these 5 assets

| id | name | type | zone |
|----|------|------|------|
| printer-3f | Printer · 3rd floor East | printer | 3F-East |
| bathroom-2f | Bathroom · 2nd floor | bathroom | 2F-Central |
| meeting-4f | Meeting room · 4th floor | meeting_room | 4F-North |
| pump-basement | Pump room · Basement | pump | B1-Mechanical |
| kitchen-1f | Kitchen · Ground floor | kitchen | 1F-West |

## Issue options per asset type

**printer:** Out of paper · Jammed · Offline · Toner low  
**bathroom:** No soap · Leak · Blocked · Needs cleaning  
**meeting_room:** Projector broken · Too cold/hot · Needs reset · (add "Other" as 4th)  
**pump:** Unusual noise · Leak visible · Not running · (add "Other" as 4th)  
**kitchen:** Empty cups/water · Appliance broken · Spill · Needs cleaning  

## Routing logic

Each issue maps to route: `inhouse` or `external`.

**External contractor** (route = external):
- Leak, Blocked, Unusual noise, Not running, Too cold/hot, Projector broken, Appliance broken

**In-house facility manager** (route = inhouse):
- Everything else (Out of paper, Jammed, Offline, Toner low, No soap, Needs cleaning, Empty cups/water, Spill, Needs reset, Other)

On submit:
1. Save report to database (asset_id, issue_label, route, timestamp)
2. POST to Slack webhook — use env var SLACK_WEBHOOK_INHOUSE for inhouse, SLACK_WEBHOOK_EXTERNAL for external
3. If webhook URL is missing, still save report and show success (graceful fallback)

## Slack message format

```
🔧 New issue · {asset name}
Issue: {issue label}
Zone: {zone}
Reported: {formatted datetime}
Asset ID: {asset_id}
Route: {In-house FM | External contractor}
```

Use Slack mrkdwn. Include emoji on first line.

## Data model

**assets** — id (text PK), name, type (enum), zone, created_at  
**reports** — id (uuid), asset_id (FK), issue_label, route (inhouse|external), created_at  

Seed assets on first deploy. Reports append-only.

## QR code helper — `/admin/qr`
- Simple page listing all 5 assets with their full URLs and a QR code image for each (use a QR library or API)
- We will print these for physical demo stickers

## Design requirements

- Clean, professional, not playful — facility management audience
- High contrast, large typography for issue buttons
- Works on iPhone Safari and Android Chrome without install
- Dark text on light background (readable in office lighting)
- Primary action color: teal or blue (trust/safety feel)
- No hamburger menus, no complex navigation — reporter sees one page only

## Technical constraints

- Use Supabase for database (assets + reports tables)
- Edge function or server action for Slack webhook POST (never expose webhook URLs client-side)
- Environment variables: SLACK_WEBHOOK_INHOUSE, SLACK_WEBHOOK_EXTERNAL
- Mobile viewport optimized; test at 390px width
- Total reporter flow: scan → tap → success in < 3 seconds on good network

## Do NOT build (out of scope)

- User accounts / authentication
- Ticket editing, assignment, or status workflow
- Photo upload
- Multi-building / multi-tenant admin
- Sensor integration or dashboards
- Push notifications
- Contractor SLA or escalation rules

## Demo context

Hackathon judges will scan a QR code on a physical printer sticker, tap "Out of paper", and expect a Slack message in #facility within seconds. Second demo: scan bathroom QR, tap "Leak", message goes to contractor channel instead. Build for live demo reliability.
```

---

## Validation map

Use this after Lovable generates the first prototype. Check each item before calling the build demo-ready.

### A. Product validation (does it work?)

| # | Test | Pass criteria | How to test |
|---|------|---------------|-------------|
| P1 | Asset page loads | `/r/printer-3f` shows correct name, zone, type | Open URL on phone |
| P2 | Issue grid matches type | Printer shows 4 printer issues; bathroom shows 4 bathroom issues | Visit each of 5 asset URLs |
| P3 | One-tap submit | Single tap → success screen, no form fields | Tap any issue |
| P4 | In-house routing | "Out of paper" on printer → route = inhouse | Check admin table + Slack |
| P5 | External routing | "Leak" on bathroom → route = external | Check admin table + Slack |
| P6 | Slack delivery | Message appears in correct channel within 3s | Live test with webhooks configured |
| P7 | Graceful fallback | Submit works and saves even if Slack webhook missing | Temporarily unset env var |
| P8 | QR codes printable | `/admin/qr` shows scannable codes for all 5 assets | Scan with phone camera |
| P9 | Mobile performance | Page loads < 2s, buttons easy to tap | iPhone Safari, one hand |
| P10 | Admin backup | `/admin` lists all submitted reports with timestamp | Submit 2 issues, refresh |

### B. Problem validation (does the demo tell the story?)

| # | Criterion | Pass criteria | Demo beat |
|---|-----------|---------------|-----------|
| B1 | Zero friction | Reporter never types, never logs in | Judge scans → taps → done |
| B2 | Location implicit | Asset context visible before tap | Page shows "Printer · 3rd floor East" |
| B3 | Right person | Different issues reach different responders | Printer vs bathroom contrast |
| B4 | Reactive → better | Narrative: "reporting is painful today; this removes it" | 90s demo script |
| B5 | Predictive hook | Close with: "predictive layer comes next" | Verbal — not in app yet |

### C. Market validation (pitch evidence — gather outside Lovable)

| # | Signal | Status | Source to cite |
|---|--------|--------|----------------|
| V1 | Incumbent exists | ☐ | Facilio, Planon, ServiceNow have QR + ticketing |
| V2 | Gap we claim | ☐ | One-tap route to *right* responder without FM triage |
| V3 | Market size stat | ☐ | Facility management / smart building TAM stat |
| V4 | Mentor or user quote | ☐ | Sat mentor conversation at The Shack |
| V5 | Competitor screenshot | ☐ | Show 3+ step form vs our 1 tap |

> Lovable builds the product; your team still owns V1–V5 for judging criterion #3.

### D. Speed & demo validation (ready for Sat 20:00 / Sun 16:00)

| # | Item | Pass criteria | Owner |
|---|------|---------------|-------|
| D1 | End-to-end latency | Scan → Slack < 3 seconds | 🤖 test before Pitch & Dine |
| D2 | Physical QR stickers | 5 printed codes taped to demo props | 🧑 print from `/admin/qr` |
| D3 | Slack channels live | `#facility` + `#contractors` (or DMs) on projector | 🧑 create webhooks |
| D4 | Demo script rehearsed | 90s flow without dead ends | 🤝 team |
| D5 | Backup plan | Admin page works if Slack fails | 🤖 verify P7 |
| D6 | Two-scenario demo | In-house issue + external issue back-to-back | 🤝 run full script |
| D7 | Product name visible | "Z2D Lifecycle" on landing page | 🤖 check header |

### E. Z2D judging scorecard (post-build self-review)

Score 1–5 after first working prototype. **Fix the lowest score first.**

| Criterion | Question | Target score | Notes |
|-----------|----------|--------------|-------|
| **PRODUCT** | Does scan → tap → Slack work reliably on a phone? | ≥ 4 | |
| **PROBLEM** | Does demo show reactive reporting pain solved in a novel way? | ≥ 4 | Contrast with form-based tools |
| **VALIDATION** | Do we have 2+ market signals beyond "we built it"? | ≥ 3 | Weakest — fill V1–V5 |
| **SPEED & DEMO** | Can a judge try it live in 90 seconds? | ≥ 5 | This wedge is built for this |

---

## Post-Lovable setup checklist

1. **Redeem credits** — code `COMM-ZD2-MAPJ` → lovable.dev → Settings → Plans & Credits
2. **Create Slack incoming webhooks** — one for in-house, one for contractors
3. **Set env vars** in Lovable: `SLACK_WEBHOOK_INHOUSE`, `SLACK_WEBHOOK_EXTERNAL`
4. **Print QR codes** from `/admin/qr` — tape to printer, bathroom sign, etc.
5. **Run validation map** sections A + D before Pitch & Dine
6. **Gather validation signals** (section C) during mentor sessions Sat afternoon

---

## Open decisions (resolve before send)

| Decision | Recommendation | Why |
|----------|----------------|-----|
| App host | **Lovable** | You're already here; fastest path to mobile web |
| Slack channels | **Two webhooks** | Cleaner demo contrast on projector |
| Demo props | **Printed asset cards + 1 real printer** | Reliable at The Shack |
| Product name | **Z2D Lifecycle** | Matches project; rename later if needed |

---

## Related

- [[MVP-FLOW]] — full flow spec
- [[ACTIVE_PLAN]] — hackathon timeline
- [[06-Wiki/Problem]] — problem definition
- [[04-Resources/Z2D/credits-and-resources]] — Lovable credit redemption
