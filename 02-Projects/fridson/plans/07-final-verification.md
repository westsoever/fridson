# Phase 7 — Final Verification

**Goal:** Full dry-run of the 3-minute pitch — timing, fallbacks, and make-plan final verification. Last gate before Sun 16:00 live demo.

**Prerequisites:** Phases 1, 2, 3 complete. Phase 4 logistics armed. Phase 6 docs updated (recommended).

---

## Agent pickup instructions

> You are executing **Phase 7** (final verification). Read Phase 0 + [[../pitch/script|script]]. Run the dry-run checklist; fix **show-stopper bugs only**. Do not start new features. Report pass/fail with evidence.

---

## Sources consulted

| Source | Purpose |
|--------|---------|
| `02-Projects/fridson/pitch/script.md:72-79` | Timing budget |
| `02-Projects/fridson/ACTIVE_PLAN.md:186-198` | Phase 7 + final verification |
| `02-Projects/fridson/plans/03-verify-live-demo-path.md` | E2E checklist (re-run) |
| `02-Projects/fridson/plans/04-pitch-logistics.md` | T-10 checklist |
| make-plan skill | Final phase: verify, grep anti-patterns, run tests |

---

## What to implement

**Verification only** — copy make-plan Final Phase (`make-plan/SKILL.md:45-49`):

1. Verify implementations match documentation
2. Check anti-patterns (grep)
3. Run tests to confirm functionality

---

## Pre-dry-run build verification

```bash
cd /Users/clyde/fridson/fridson-app
bun run build
cd supabase/functions/agent && deno task test
```

Expected: build exit 0; 10/10 agent tests pass.

---

## Anti-pattern grep (must be clean or explained)

```bash
cd /Users/clyde/fridson/fridson-app

# No invented route/status values in app code
rg '"in-house"|"contractor"' src/ --glob '!*.test.*'
# Expect: no matches (use inhouse/external)

# Dual invoke documented or resolved
rg "invokeResolutionAgent" src/
# Expect: single call site in reports.functions.ts (Phase 2 decision)

# No force-push artifacts
git log -1 --oneline
```

---

## Full dry-run script (3:00 timing)

Run with **full team** on **real hardware** before 16:00.

| Section | Budget | Cumulative | Verify |
|---------|--------|------------|--------|
| Minute 1 — live demo | 60s | 1:00 | Scan → projection → approve |
| Minute 2 — ecosystem | 60s | 2:00 | Lenses or slide fallback |
| Minute 3 — business case | 60s | 3:00 | Numbers from business-case.md |

**Stopwatch each section.** Total must hit **3:00 ±5s** (re-trim script if needed).

### Minute 1 live beats (script.md:26-30)

1. [ ] Narration 0:00–0:20 (hassle setup)
2. [ ] Scan `meeting-4f` QR → tap "Projector broken" → "Sent."
3. [ ] Projection: marker on 4F + structured report in feed
4. [ ] Feed: providers → RFQ → bids → negotiate → slot
5. [ ] Presenter taps Approve → "Technician booked"
6. [ ] Whole Minute 1 ≤ 60s

### Fallback tests (run once each)

| Failure mode | Fallback | Works? |
|--------------|----------|--------|
| Scan fails | Bookmark `/r/meeting-4f` | [ ] |
| Network slow | Pre-recorded 60s clip | [ ] |
| Feed stalls | Mock projection / Replay | [ ] |
| Agent error | Workspace shows prepared data | [ ] |
| Total live failure | Full recording + live narration | [ ] |

### Minute 2 (≤60s)

- [ ] Stakeholder lenses OR static slide
- [ ] Triage-shift line verbatim (`ecosystem.md:53`)

### Minute 3 (≤60s)

- [ ] Three numbers: cost ↓, time ↓, 80% quality
- [ ] Sources ready if questioned (`business-case.md`)

---

## T-10 stage checklist

Copy from [[04-pitch-logistics|Phase 4]] §F — run immediately before judging slot.

---

## Final verification checklist (whole pitch)

From `ACTIVE_PLAN.md:195-198`:

- [ ] End-to-end dry-run hits exactly 3 minutes
- [ ] Every live beat has a tested fallback
- [ ] Each minute maps to its source-of-truth section
- [ ] Milestone 2 submitted (15:00)
- [ ] Day 2 check-in done
- [ ] Brand spelling consistent everywhere
- [ ] `/projection?feed=real` confirmed on venue network

---

## Anti-pattern guards

- ❌ Do not skip fallback tests — "works on hotel Wi-Fi" ≠ venue
- ❌ Do not improvise business-case numbers on stage
- ❌ Do not extend scope during dry-run fixes
- ❌ Do not mark Phase 7 complete if Minute 1 live path untested

---

## Completion report template

```markdown
## Phase 7 — Dry-run report (2026-06-28)

- Timing: M1 __s / M2 __s / M3 __s / Total __s
- Live path: PASS | FAIL (notes)
- Fallbacks tested: [list]
- Blockers for 16:00: [none | …]
- Agent path used: A | B | C (Phase 2)
```

---

## Documentation references

- [[../pitch/script|pitch/script.md]]
- [[../pitch/logistics|pitch/logistics.md]]
- [[../pitch/business-case|pitch/business-case.md]]
- [[03-verify-live-demo-path|Phase 3 checklist]]

---

## After Phase 7

**Live demo Sun 16:00.** Presenter follows script; tech runs projection + workspace tabs. Good luck.
