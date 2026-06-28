# Phase 1 — Deploy Gates

**Goal:** Push app to Lovable, apply migrations to live Supabase, deploy edge functions, set secrets — so the demo runs on production infrastructure.

**Prerequisites:** Phase 0 ([[00-documentation-discovery|00-documentation-discovery]]) read. Authenticated access to Supabase CLI and app git push.

**Blocks:** Phases 2, 3, 7.

---

## Agent pickup instructions

> You are executing **Phase 1**. Read Phase 0 first. You may edit `fridson-app/` for merge conflict resolution only. Do **not** change agent trigger logic (Phase 2) or pitch docs (Phase 4/6). Run git sync before any push.

---

## Sources consulted

Reference [[00-documentation-discovery#sources-consulted|Phase 0 sources]], plus:

| Source | Relevant section |
|--------|------------------|
| `02-Projects/fridson/ACTIVE_PLAN.md:248-266` | Blockers — push, migrations, deploy, secrets |
| `fridson-app/HANDOFF.md:40-55` | Deploy checklist, secrets list |
| `fridson-app/supabase/config.toml` | Project ref, function JWT settings |
| `fridson-app/AGENTS.md` | Lovable: no force-push |

---

## What to implement

Copy these exact steps from docs — do not invent alternate deploy paths.

### Step 1 — Reconcile git divergence (BLOCKER)

**Fact:** Local and `origin/main` each have 3 commits after `fd3caeb` (Phase 0).

```bash
cd /Users/clyde/fridson/fridson-app
git fetch --all --prune
git status
git log --oneline --graph --left-right HEAD...origin/main
```

**Copy pattern:** merge (not rebase) per vault git-sync rule:

```bash
git merge origin/main -m "Merge origin/main (Lovable sync) with local schematic commits"
# Resolve conflicts if any — prefer keeping BOTH schematic routes and Lovable UI changes
bun run build   # must pass before push
```

**Anti-pattern:** `git push --force` — forbidden on Lovable-connected branch (`AGENTS.md`).

### Step 2 — Push to Lovable

```bash
cd /Users/clyde/fridson/fridson-app
git push origin main
```

**Verify:** Lovable rebuild starts; live app at https://fridson.lovable.app reflects schematic + latest main.

### Step 3 — Apply migrations

From `ACTIVE_PLAN.md:252`:

```bash
cd /Users/clyde/fridson/fridson-app
bunx supabase@latest link --project-ref yyidatcqbvsbntdavmww
bunx supabase@latest db push
```

**Alternative:** Lovable Supabase sync (if CLI auth unavailable).

**Key migrations to confirm applied:**

| File | Purpose |
|------|---------|
| `20260627190000_track1_assets_location.sql` | Asset coords |
| `20260627190200_track1_providers.sql` | 55 providers |
| `20260627190300_track1_events.sql` | `events` table + report triggers |
| `20260627180100_report_agent_webhooks.sql` | pg_net → process-triage/research |
| `20260627200000_triage_operations.sql` | Urgency, audit, acknowledge |

### Step 4 — Deploy edge functions

From `ACTIVE_PLAN.md:253` and `HANDOFF.md:48`:

```bash
cd /Users/clyde/fridson/fridson-app
bunx supabase@latest functions deploy agent process-triage process-research
```

Config already sets `verify_jwt = false` (`config.toml:6-15`).

### Step 5 — Set function secrets

From `ACTIVE_PLAN.md:254` + `HANDOFF.md:42-47`:

**Required (dashboard or CLI):**

```bash
bunx supabase@latest secrets set LOVABLE_API_KEY=<key>
```

**For webhook agents (HANDOFF.md):**

```bash
bunx supabase@latest secrets set FIRECRAWL_API_KEY=<key>
# SLACK removed from app per ACTIVE_PLAN — skip SLACK_API_KEY unless re-added
```

**Optional — real RFQ email (resolution agent):**

```bash
bunx supabase@latest secrets set RESEND_API_KEY=<key>
bunx supabase@latest secrets set AGENT_LIVE_EMAIL=1
# Optional: AGENT_LIVE_TO=demo-vendor@yourinbox.com
```

`SUPABASE_URL` and `SUPABASE_SERVICE_ROLE_KEY` are auto-injected.

**Optional hardening** (`HANDOFF.md:57-66`): `WEBHOOK_SECRET` + `ALTER DATABASE postgres SET app.webhook_secret = '…'`.

---

## Documentation references

- `02-Projects/fridson/ACTIVE_PLAN.md` — Blockers section
- `fridson-app/HANDOFF.md` — full webhook deploy checklist
- `fridson-app/supabase/functions/agent/README.md` — agent env vars
- `fridson-app/supabase/config.toml` — project_id

---

## Verification checklist

Run after all steps:

### Build

```bash
cd /Users/clyde/fridson/fridson-app
bun run build
```

Expected: exit 0.

### Git

```bash
git status   # clean, up to date with origin/main
git log -1 --oneline
```

### Migrations (if CLI linked)

```bash
bunx supabase@latest migration list
# Or SQL: SELECT EXISTS (SELECT 1 FROM information_schema.tables WHERE table_name = 'events');
```

### Edge functions

```bash
curl -s "https://yyidatcqbvsbntdavmww.supabase.co/functions/v1/agent" \
  -H "apikey: $SUPABASE_PUBLISHABLE_KEY"
```

Expected: JSON health response (not 404).

```bash
# process-triage is DB-triggered; smoke via submitReport in Phase 3
```

### Live routes (browser)

- [ ] https://fridson.lovable.app/r/meeting-4f loads
- [ ] https://fridson.lovable.app/projection loads (mock feed)
- [ ] https://fridson.lovable.app/schematic loads (after push)
- [ ] https://fridson.lovable.app/workspace loads

### Secrets

- [ ] `LOVABLE_API_KEY` set (triage works)
- [ ] Document which optional secrets were set (Resend, Firecrawl)

---

## Anti-pattern guards

- ❌ Do not skip merge — pushing local-only commits over Lovable sync loses work
- ❌ Do not force-push main
- ❌ Do not commit service-role keys to `.env` in repo
- ❌ Do not change `submitReport` / agent invoke in this phase (Phase 2)
- ❌ Do not assume migrations applied without verification query

---

## Handoff to Phase 2

When complete, report:

1. Merge commit hash (if any)
2. Push confirmed on origin/main
3. Migration list status (applied / pending)
4. Functions deploy output
5. Secrets set (names only, not values)
