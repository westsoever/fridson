# Deploy Blocker Report — 2026-06-28 (updated)

**Status:** Frontend pushed ✅ `b0185f3` · Supabase CLI blocked ❌ · Lovable rebuild in progress

## Completed (this session)

| Step | Result |
|------|--------|
| Approve→agent→email wired + committed | ✅ `b0185f3` |
| `git push origin main` | ✅ Lovable rebuild triggered |
| `bun run build` | ✅ exit 0 |
| Agent Deno tests | ✅ 12/12 (local) |
| Live `/projection` | ✅ loads (scripted demo mode until `?feed=real` + migrations) |

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

# 4. Deploy edge functions
bunx supabase@latest functions deploy agent process-triage process-research

# 5. Set secrets (names only — fill values in dashboard or CLI)
bunx supabase@latest secrets set LOVABLE_API_KEY=<key>
bunx supabase@latest secrets set FIRECRAWL_API_KEY=<key>
# Mock RFQ email on Approve (recommended for demo):
bunx supabase@latest secrets set RESEND_API_KEY=<key>
bunx supabase@latest secrets set AGENT_MOCK_INBOX=<team inbox e.g. chrisw0129@gmail.com>
```

**Alternative:** Lovable dashboard → Supabase sync (migrations + functions) — often faster than CLI when token is blocked.

## Verify after deploy

See [[LIVE-VERIFY-RUNBOOK]] for full E2E steps.

Quick checks:

```bash
cd /Users/clyde/fridson/fridson-app && source .env
curl -s "https://yyidatcqbvsbntdavmww.supabase.co/functions/v1/agent" \
  -H "apikey: $VITE_SUPABASE_PUBLISHABLE_KEY" \
  -H "Authorization: Bearer $VITE_SUPABASE_PUBLISHABLE_KEY"
```

## E2E demo path (Phase 3 — after deploy)

1. Open `https://fridson.lovable.app/projection?feed=real` + **Replay**
2. Scan `https://fridson.lovable.app/r/meeting-4f` → tap **"Projector broken"**
3. Wait for `awaiting_approval` in `/workspace`
4. Click **Approve & dispatch agent** → confirm RFQ in `AGENT_MOCK_INBOX`
5. Confirm events in projection feed within ~60s
6. Fallback: `/projection` without `?feed=real` (mock timeline)

## Agent path (resolved)

**Approve-triggered:** submit → triage webhook only; Approve → resolution agent + `auto_confirm` + process-research webhook. Pushed in `b0185f3`.
