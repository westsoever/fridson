# Track 2 — Schematic & Projection

**Owner:** Slavi · **Mission:** Build the **screen behind the presenter** — the building schematic with a live location pinpoint, plus the activity-feed projection that turns Tracks 1–3 into one ≤60s visual story. This is the beat that makes the demo *click*.

> Read [[INTERFACES]] §2 (coords) + §4 (event feed). Build against **mock events** first so you don't wait on Track 3.

---

## You own
- `/schematic` page/components (floorplan render + marker/pulse)
- `/projection` page/components (stage view: schematic + live step-card feed)
- A small **mock event emitter** for local dev (delete/disable once Track 3 is live)

## You must NOT touch
- DB schema (ask Track 1) · agent service `/agent` (Track 3) · deck/`pitch/` (Track 4)

## Depends on
- Track 1: floorplan image + asset `location` coords
- Track 3: real events on the feed (you can stub these until then)

---

## Tasks (P2 #2 + P4 #8)
- [ ] Render the floorplan; place a **marker** using `location.x/y` × rendered size (per [[INTERFACES]] §2)
- [ ] On `report.created` / `location.pinpointed`, **pulse the marker** at the asset spot within ~2s
- [ ] Build the **projection view**: schematic + an ordered **activity feed** of step cards (one card per event in [[INTERFACES]] §4)
- [ ] Wire the feed to the event channel (websocket/poll the `events` table); **scripted timeline as fallback**
- [ ] Tune pacing so the whole sequence is visible + readable in **≤60s**, legible from stage (large type, clear step states)
- [ ] *(stretch, only if time)* light per-ticket "context record" view for Minute 2 — content/script comes from Track 4

## Acceptance
- [ ] Scanning `printer-3f` drops a marker on the printer's spot within ~2s; legible when projected (test at distance)
- [ ] **One scan** drives the entire projected sequence end-to-end with **no extra clicks**, total ≤60s
- [ ] Renders gracefully if an event is missing (show what arrived)

## Guards
- No raw logs/JSON on stage — human-readable step cards only. Don't block on Track 3: mock the events. Don't change the event shape unilaterally — propose in [[INTERFACES]].
