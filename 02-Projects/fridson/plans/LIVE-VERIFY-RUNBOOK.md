# Live Verify Runbook — Post-Deploy E2E

**Prerequisites:** App pushed (`b0185f3`+ on `origin/main`), Lovable rebuild complete, Supabase migrations + edge functions deployed (Lovable sync or CLI).

**Goal:** Confirm scan → triage → **Approve → agent → mock RFQ email** → projection feed before dry-run.

---

## Gate 1 — Routes (2 min)

Open in browser (all must load):

| URL | Expect |
|-----|--------|
| https://fridson.lovable.app/r/meeting-4f | Issue picker, asset "Meeting room" |
| https://fridson.lovable.app/projection?feed=real | Schematic + feed; green "Live feed" badge |
| https://fridson.lovable.app/workspace | Triage inbox |
| https://fridson.lovable.app/schematic | Floor selector + markers |

**Fallback:** `/projection` without `?feed=real` → scripted ~54s timeline.

---

## Gate 2 — Agent health (1 min)

Supabase dashboard → Edge Functions → `agent` → Logs, or:

```bash
# From fridson-app/ with .env loaded — do not paste keys into chat
source .env
curl -s "https://yyidatcqbvsbntdavmww.supabase.co/functions/v1/agent" \
  -H "apikey: $VITE_SUPABASE_PUBLISHABLE_KEY" \
  -H "Authorization: Bearer $VITE_SUPABASE_PUBLISHABLE_KEY"
```

Expect JSON: `"ok": true`, `"events_emitted": [...]`, `"mock_email"` or `"live_email"` flags.

---

## Gate 3 — Secrets (human, Supabase dashboard)

Edge function secrets for **`agent`**:

| Secret | Required | Purpose |
|--------|----------|---------|
| `RESEND_API_KEY` | Yes (for inbox test) | Send RFQ emails |
| `AGENT_MOCK_INBOX` | Yes | Team inbox — all RFQs redirect here |
| `LOVABLE_API_KEY` | Yes | `process-triage` / `process-research` |
| `FIRECRAWL_API_KEY` | Yes | Contractor research on approve |

Optional: `AGENT_LIVE_EMAIL=1` only if sending directly to vendor addresses (not recommended for demo).

---

## Gate 4 — Hero flow (5 min)

**Asset:** `meeting-4f` → tap **"Projector broken"**

1. **Projection tab:** `https://fridson.lovable.app/projection?feed=real` → click **Replay**
2. **Phone:** scan hero QR or open `/r/meeting-4f` → tap issue → success screen instant
3. **Wait ~10s:** report appears in workspace as `awaiting_approval` (triage webhook)
4. **Workspace:** select report → **Approve & dispatch agent**
5. **Within ~30s:**
   - Audit log shows `approve_dispatch_agent`
   - Projection feed: `providers.selected` → `rfq.sent` → `bid.received` → `negotiation.round` → `slot.booked` → `pm.decision`
6. **Inbox:** open `AGENT_MOCK_INBOX` — RFQ with `[MOCK INBOX — RFQ redirect]`, report ID, provider name

**SQL check (Supabase SQL editor):**

```sql
SELECT type, ts FROM events
WHERE report_id = '<paste report uuid>'
ORDER BY ts;
```

---

## Gate 5 — Failure modes

| Symptom | Fix |
|---------|-----|
| Triage stuck on `awaiting_ai` | Deploy `process-triage`; set `LOVABLE_API_KEY` |
| Approve does nothing on feed | Deploy `agent` function; push `b0185f3`+ frontend |
| No email in inbox | Set `RESEND_API_KEY` + `AGENT_MOCK_INBOX` on `agent` |
| Feed shows mock badge | Use `?feed=real`; confirm `events` table exists (migrations) |
| 403 on Supabase CLI | Use Lovable dashboard → Supabase sync instead |

---

## Pass criteria → proceed to dry-run

- [ ] Hero scan completes in < 3s on venue Wi-Fi
- [ ] Approve dispatches agent without page hang
- [ ] RFQ email in team inbox OR stub labelled in `events` payload (`mode: mock`)
- [ ] Projection shows full sequence ≤ ~60s
- [ ] Fallback tabs armed per [[../pitch/dry-run-checklist]]
