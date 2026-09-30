# Gnosis Lab factory → cloud Routine (migration plan, 2026-09-30)

Why: the factory is a Cowork "task on this computer". Those are deprecated (no new ones after
Oct 6) and the Gnosis one has not fired since the peacock run on Sept 25. The Ashborn factory was
already moved to a Routine on Sept 27. This moves Gnosis too, but into the cloud, so it no longer
depends on the Mac being awake.

Rule for the whole migration: **the pipeline mechanics do not change.** Same prompt, same rules,
same models, same scripts, same VESPER voice, same stitch/mix/watermark chain. The only things
that change are *where it runs* (a cloud container instead of the Mac) and therefore (a) file
paths, (b) where secrets come from, (c) a `git push` at the end of each run so the logs and
learnings persist.

Keep the old task enabled until the first cloud run has produced and queued an episode. Then
disable it. The old task is the rollback until Oct 6.

---

## Part A — on the Mac (Wilder, ~15 min)

### A1. Create the private repo and push the pipeline

```bash
cd "/Users/mac/Claude/Projects/Gnosis Lab"

# 1. Keep code, specs, logs and small brand assets. Exclude renders, clips, VO and secrets.
cat > .gitignore <<'EOF'
# secrets
.env
.env.*
# rendered media (regenerated every run; too big for git)
*.mp4
*.mov
*.wav
*.mp3
*.png
*.jpg
*.jpeg
*.webp
# but keep the brand kit and score bed — the pipeline needs them
!_pipeline/brand/**
!_pipeline/audio_kit/**
!_pipeline/fonts/**
# staging / deploy folders are media-only
review/
approved/
deployed/
node_modules/
.DS_Store
EOF

# 2. Poppins-Bold must travel with the repo (the stitch step hardcodes it).
mkdir -p _pipeline/fonts
cp "$(fc-list | grep -i 'Poppins-Bold' | head -1 | cut -d: -f1)" _pipeline/fonts/Poppins-Bold.ttf
ls -la _pipeline/fonts/

# 3. Find every hardcoded Mac path — paste this output to Claude, these lines get fixed in the cloud copy.
grep -rn "/Users/mac" _pipeline/ episodes/*/build/*.sh 2>/dev/null | grep -v node_modules

# 4. Find which env vars the scripts read — these become environment secrets in Part B.
grep -rhn "process.env\.[A-Z_]*" _pipeline/*.mjs | grep -o "process.env\.[A-Z_]*" | sort -u

# 5. Check the size before pushing (should be tens of MB, not GB).
git init -q 2>/dev/null; git add -A -n | wc -l; du -sh --exclude=review --exclude=approved --exclude=deployed .

# 6. Create the private repo on GitHub as ashbornstudios/gnosis-lab (web UI or gh), then:
git add -A
git commit -m "Gnosis Lab pipeline — initial import from the Mac (2026-09-30)"
git branch -M main
git remote add origin https://github.com/ashbornstudios/gnosis-lab.git
git push -u origin main
```

If step 5 shows hundreds of MB, something media-shaped slipped through: run
`git ls-files | xargs -I{} du -k {} | sort -rn | head` and add the offenders to `.gitignore`.

### A2. Give Claude access to the repo
On https://github.com/apps/claude/installations/select_target add `gnosis-lab` to the Claude
GitHub App. Then in this session say "repo pushed" and I attach it, fix the paths from A1 step 3,
and push those fixes.

---

## Part B — the cloud environment (Wilder, ~10 min, in claude.ai/code → Environments)

Create a **new** environment named `Gnosis Factory` (do not change `Default`).

**Network access:** custom allowlist (or broader), including at least:
```
api.elevenlabs.io
ashborn-os.vercel.app
*.supabase.co
d8j0ntlcm91z4.cloudfront.net        # Higgsfield generation results
d2ol7oe51mr4n9.cloudfront.net       # Higgsfield uploads
*.s3.amazonaws.com                   # Higgsfield presigned uploads
github.com
registry.npmjs.org
```
(The Default environment blocks the Higgsfield CDNs today; that is why clips had to be stitched
inside Higgsfield's sandbox during this session.)

**Environment variables / API credentials** — the names from A1 step 4. Expected:
```
ELEVENLABS_API_KEY
CRON_SECRET
NEXT_PUBLIC_SUPABASE_URL
SUPABASE_SERVICE_ROLE_KEY
```
Never paste the values into chat; they go into the environment settings only.

**Setup script:**
```bash
set -e
apt-get update -qq && apt-get install -y -qq ffmpeg fontconfig >/dev/null
mkdir -p /usr/local/share/fonts && cp /home/user/gnosis-lab/_pipeline/fonts/*.ttf /usr/local/share/fonts/ && fc-cache -f >/dev/null
cd /home/user/gnosis-lab/_pipeline && [ -f package.json ] && npm ci --silent || true
ffmpeg -version | head -1
```

**Repository:** `ashbornstudios/gnosis-lab`, branch `main`.

---

## Part C — the Routine (Claude, once A and B are done)

- Prompt: `ROUTINE_PROMPT.md` in this folder (the v4 prompt verbatim, plus a "Cloud run" header).
- Schedule: nightly, `CRON_TZ=America/Los_Angeles 0 2 * * *` (the Mac runs started ~02:15–02:45 PT).
  Change this if the old task ran at a different hour.
- Fresh session per fire, environment `Gnosis Factory`, connector: Higgsfield only.
- Push + email notification on each run's summary.

**First run is supervised:** I fire it manually while Wilder is awake, we both read the summary,
and only when it has queued an episode (`✓ queued → scheduled_posts <id>` for YouTube and the
Reel) does the old Mac task get disabled.

---

## What the Mac still owns after this
Nothing in the nightly loop. `Projects/Gnosis Lab` on the Mac becomes a mirror: `git pull` to see
the latest logs/scripts, and drop finished renders there if you want local copies (the cloud run
keeps its renders only for the session; the upload that matters goes to Supabase storage via
`queue_youtube.mjs`, exactly as before).

## Known differences to accept (mechanics unchanged, plumbing changed)
1. Paths: `/Users/mac/Claude/Projects/Gnosis Lab/` → `/home/user/gnosis-lab/`.
2. Secrets: environment variables instead of `Projects/Gnosis Lab/.env`.
3. End of run: `git add -A && git commit && git push` so `episode_log.json`, `TOPIC_BANK.md`,
   `LEARNINGS.md`, `_pipeline/analytics/latest.json` and the episode's markdown persist.
4. Renders are not kept between runs. Backlog handling (STEP −1) still works because it keys off
   `PROMPTS_READY.md` + the absence of an export, and re-renders from PROMPTS_READY verbatim.
