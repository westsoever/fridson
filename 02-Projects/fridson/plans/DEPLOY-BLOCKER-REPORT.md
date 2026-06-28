# Deploy Blocker Report — 2026-06-28

**Status:** Frontend pushed ✅ · Supabase CLI blocked ❌

## Completed

| Step | Result |
|------|--------|
| Git merge `origin/main` + schematic | ✅ `6b50e0c` |
| `git push origin main` | ✅ Lovable rebuild triggered |
| `bun run build` | ✅ exit 0 |
| Live routes HTTP | ✅ `/r/*` 200, `/projection` 200, `/schematic` 200 |

## Blocked — needs human credentials

Supabase CLI returned **403** (account lacks project privileges). Run these with a token that has access to project `yyidatcqbvsbntdavmww`:

```bash
# 1. Authenticate (one-time)
export SUPABASE_ACCESS_TOKEN="<from https://supabase.com/dashboard/account/tokens>"
cd /Users/clyde/fridson/fridson-app

# 2. Link project
bunx supabase@latest link --project-ref yyidatcqbvsbntdavmww

# 3. Apply migrations (22 files in supabase/migrations/)
bunx supabase@latest db push
# Or set SUPABASE_DB_PASSWORD if prompted

# 4. Deploy edge functions
bunx supabase@latest functions deploy agent process-triage process-research

# 5. Set secrets (names only — fill values in dashboard or CLI)
bunx supabase@latest secrets set LOVABLE_API_KEY=<key>
bunx supabase@latest secrets set FIRECRAWL_API_KEY=<key>
# Optional mock RFQ email:
bunx supabase@latest secrets set RESEND_API_KEY=<key>
bunx supabase@latest secrets set AGENT_LIVE_EMAIL=1
```

**Alternative:** Lovable Supabase sync in dashboard (migrations + functions) if CLI unavailable.

## Verify after deploy

```bash
# Agent health
curl -s "https://yyidatcqbvsbntdavmww.supabase.co/functions/v1/agent" \
  -H "apikey: $VITE_SUPABASE_PUBLISHABLE_KEY"

# Events table exists
bunx supabase@latest db execute --sql \
  "SELECT EXISTS (SELECT 1 FROM information_schema.tables WHERE table_name = 'events');"

# Agent offline tests (requires deno)
cd supabase/functions/agent && deno task test
```

## E2E demo path (Phase 3 — manual after deploy)

1. Open `https://fridson.lovable.app/projection?feed=real` + Replay
2. Scan `https://fridson.lovable.app/r/meeting-4f` → tap "Projector broken"
3. Confirm events in feed within ~60s
4. Open `/workspace` → Approve on `awaiting_approval` ticket
5. Fallback: `/projection` without `?feed=real` (mock timeline)

## Agent path decision (Phase 2)

**Option A (hybrid)** — documented in `reports.functions.ts`:
- Webhook `process-triage` → workspace AI fields
- `invokeResolutionAgent` → `events` → `/projection?feed=real`
