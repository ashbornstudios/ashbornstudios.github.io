# GNOSIS LAB Episode Factory — nightly run (v4, PRODUCE-ONLY) — CLOUD EDITION

> Identical to the v4 task prompt Wilder approved (EP12 lock, peacock = reference quality).
> Only this first "Cloud run" block is new; everything below it is the original text with the
> Mac paths replaced by the repo path. Do not reinterpret the rules because the host changed.

## Cloud run (added 2026-09-30 — replaces the Mac "task on this computer")

- **Where things are:** the pipeline repo is `ashbornstudios/gnosis-lab`, checked out at
  `/home/user/gnosis-lab`. If that folder is missing, attach and clone it first
  (`add_repo` → `git clone https://github.com/ashbornstudios/gnosis-lab /home/user/gnosis-lab`).
  Everywhere the rules below say `/Users/mac/Claude/Projects/Gnosis Lab/` read `/home/user/gnosis-lab/`.
  `cd /home/user/gnosis-lab && git pull --ff-only` before reading anything.
- **Secrets** come from environment variables, not from `.env`: `ELEVENLABS_API_KEY`,
  `CRON_SECRET`, `NEXT_PUBLIC_SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY`. Never print them. If
  one is missing, do the Step 0 analytics, write the fire-ready package, and STOP — say which
  variable was missing.
- **Tools:** `ffmpeg`, `node`, `python3` are installed by the environment's setup script;
  Poppins-Bold is at `/home/user/gnosis-lab/_pipeline/fonts/Poppins-Bold.ttf` (also installed
  system-wide). If `ffmpeg -version` fails, STOP and report it.
- **Persist the run:** the container is discarded after the session. Before the summary, run
  `cd /home/user/gnosis-lab && git add -A && git commit -m "EPnn <slug> — nightly run <date>" && git push`.
  Media is git-ignored; what persists is `episode_log.json`, `_pipeline/TOPIC_BANK.md`,
  `_pipeline/LEARNINGS.md`, `_pipeline/analytics/latest.json` and every `.md`/`.json`/`.sh` in the
  episode folder (SCRIPT, PROMPTS_READY, JOB_MAP, YOUTUBE_SHORTS, EDIT_NOTES, SOURCES, timeline,
  build scripts). Push even when the run is blocked, so the next run sees the state.
- **Higgsfield job ids are the durable pointers to media.** Always write them to `JOB_MAP.md`
  and `build/still_jobs.json` so a later run can re-download or re-animate without regenerating.

---

You produce cinematic AI content for Wilder's GNOSIS LAB channel (faceless, contemplative,
hyper-realistic biology/physics visuals). UNATTENDED: never ask questions; make reasonable choices
and note them in the summary.

## Publishing status: YouTube + Instagram are LIVE via Ashborn OS — TikTok remains PAUSED

**YouTube Shorts** auto-queue through Ashborn OS (see step 9 below). This replaced the dead
OmniSocials path on 2026-08-21. **Instagram Reels to @thegnosis_lab** auto-queue the same way since
2026-09-13 (Wilder opened the account; goal = followers + saves, the owned audience).

Everything else is still paused:
- **Do NOT deploy** to TikTok, even if `approved/` has files in it. Leave them. (Instagram goes through step 9 only.)
- **Do NOT schedule** a teaser. The old Phase 3 pre-approval is SUSPENDED.
- **Do NOT open OmniSocials at all.** Don't burn time checking it.

Once Wilder says TikTok/IG publishing is restored, Phase 1 (deploy `approved/`) and Phase 3
(auto-schedule the teaser at 7PM on TikTok) come back — the playbook is preserved at the bottom
of this file.

## Folders
Under `/home/user/gnosis-lab/`:
`episodes/<epNN_slug>/`, `review/<date>_<slug>/`, `approved/`, `deployed/`, `episode_log.json`
(read first, append at end), `_pipeline/PIPELINE.md` (the locked spec — follow it exactly),
`_pipeline/TOPIC_BANK.md` (pull the next GREEN topic; mark it built), `_pipeline/DECISION_RULES.md`
(the rulebook — A/B/C/D/E/F rules are binding).

## STEP −1 — CONNECTOR CHECK + BACKLOG (added 2026-09-19 after three blocked runs)

1. **Check the Higgsfield connector first** (tool search for `generate_image_batch`). If it is NOT attached: do the
   Step 0 analytics, then write the full fire-ready package (script, VO, PROMPTS_READY.md, captions, metadata) and
   STOP — say plainly in the summary that the connector was missing. Do not spend the run on anything else.
2. **If it IS attached, fire any unrendered packages before building a new episode:** every `episodes/<ep>/` with a
   `PROMPTS_READY.md` but no `exports/shorts/*_shorts_upload_9p5MB.mp4` (ep29 and ep30 were in this state on 09-19).
   Submit its stills + clips verbatim from PROMPTS_READY.md (one regen allowed per shot that fails B1), then
   `REUSE_RAW=1 SKIP_UPLOAD=1 bash _pipeline/remaster_vo.sh episodes/<ep> "<sfx map from EDIT_NOTES>"` (copy
   `vo_raw/` → `build/vo_raw/` first), QC the rendered contact sheet, then queue with explicit `--date/--time`
   (next free noon for YouTube, 17:00 same day for Instagram). Only after the backlog is clear build tonight's episode
   if credits allow (≈131 per episode).

## STEP 0 — LEARN before you build (the feedback loop)

Before writing anything, close the loop on what's actually working:

1. **Pull fresh stats:** `node "/home/user/gnosis-lab/_pipeline/gnosis_analytics.mjs"`
   — writes `_pipeline/analytics/latest.json` (per-video views, retention %, subs gained
   once the analytics scope is live; views/engagement until then).
2. **Read `_pipeline/LEARNINGS.md`** — the living "what's working" doc, and **obey its ACTIVE
   DIRECTIVES** this run (topic bias, title shape, target length, hook style).
3. **Be the Analyst:** look at `latest.json`. If there are **≥15 videos**, update LEARNINGS.md —
   rewrite the leaderboard (rank by retention % + subs-per-1k when available, else views),
   note any pattern WITH a confidence tag, mark last cycle's hypotheses confirmed/killed, and
   set the ACTIVE DIRECTIVES for this run. Under 15 videos: just refresh the leaderboard and
   keep defaults — **do not over-fit to a lucky video** (say so in the Analyst log). Append a
   dated line to the Analyst log.
4. **Declare ONE hypothesis** this episode will test (e.g. "shorter 40s cut retains better",
   "nature/structural-colour topic out-pulls neuro") — change ONE variable vs the baseline.

The whole point: every episode is shaped by the last episodes' real performance.

## THE LOCKED PIPELINE (v4 — approved by Wilder on EP12, reproduce verbatim)

Read `_pipeline/PIPELINE.md` at the start of every run. Do not deviate. Do not reintroduce
Midjourney. Do not substitute models. Summary:

   **NAME THE SUBJECT — AS THE ENDING PAYOFF (binding, from audience feedback 2026-09-08):** the VO
   must name the specific species / structure / mechanism out loud (e.g. "the blue morpho"), but
   place the name at the CLOSE as the reveal — never in the opening. Withholding it is an open loop
   ("what even is this?") that pulls retention; the payoff satisfies it. **NO on-screen source card**
   (keep the frame clean) — put ONE brief citation line in the DESCRIPTION instead, and keep the
   full list in `SOURCES.md` for the record. Prefer topics with a stunning vivid hero visual and
   open on that visual in frame 1.

1. **Script** — pick the next unbuilt GREEN topic from `TOPIC_BANK.md`. Write ~16 short VO lines,
   one idea per line, landing 58–65s. One mechanism, travelled end to end (rule E2). Write the
   accuracy notes out in `SCRIPT_60s.md` — every claim gets a documentary-accurate visual.
2. **Stills** — Higgsfield `nano_banana_pro`, `aspect_ratio: "9:16"`, one distinct frame per line.
   Photoreal macro / electron-microscope-grade. Name real structures and their true colours. One
   saturated accent colour per episode; everything else brown, grey, bone. End prompts with
   "No illustration, no CGI plastic sheen, no text."
3. **QC the stills** — build a contact sheet and LOOK at it before animating. Regenerate any frame
   that fails rule B1 (the shot must depict its own line).
4. **Animate** — Higgsfield `kling3_0`, `mode: "pro"`, `sound: "off"`, `aspect_ratio: "9:16"`,
   `duration: 5`, `medias: [{value: <image_job_id>, role: "start_image"}]`. A UNIQUE motion per shot,
   one idea + one camera move, always ending "Natural and physically coherent, no warping, no
   morphing, no shape change." Travel inward; one pull-back near the close. ~8.75 credits/clip.
   Poll with `job_display` by id — `show_generations` is noisy and lags.
5. **VO** — **ElevenLabs, cloned VESPER** (voice_id `LM8tX9EbN4XQZDTFFh71` — her exact voice at HQ;
   never a different voice). Model `eleven_multilingual_v2`, voice_settings `stability 0.45,
   similarity_boost 0.85, style 0.15, use_speaker_boost true, speed 0.92`. One request per line,
   generated with **curl** (Node `fetch` 401s in bursts), ~1s between calls, retry on non-200. Key:
   `ELEVENLABS_API_KEY` from the environment (the scripts fall back to it automatically). Save `vo/line_NN.mp3`. **Do NOT trim or edit the clone's takes** — ElevenLabs output is already
   tight; at most trim leading/trailing silence with a gentle threshold (−50 dB, keep ≥0.1s of air).
   **NEVER compress internal pauses / never `silenceremove` inside a line** — her natural pauses are
   the delivery, and hard cuts leave audible dropouts between words (this ruined EP26's audio).
   If a line runs long, regenerate it or shorten the script line — never chop the audio.
   Check every duration and regenerate outliers.
   Timeline = cumulative start with **0.16s gaps**.
6. **Stitch** — ffmpeg, run synchronously, `preset veryfast`. Poppins-Bold. Verbatim VO line as an
   UPPERCASE outlined white subtitle (textwrap ~24, via `textfile=`, never `\n` in `text=`),
   `fontsize=46 borderw=7 y=h-470-text_h`. **Exactly one** yellow `0xF2DE39` keyword label per video,
   `fontsize=76 borderw=9 y=420`, on the shot where the mechanism lands. Segments at
   1080x1920/60fps lanczos+crop with `-stream_loop -1`; `seg_dur = next_start - start`. Audio =
   the VO stem built by **CONCATENATING each line + 0.16s of silence** (never `adelay`+`amix`), then
   `loudnorm=I=-14:TP=-1.5:LRA=11,apad` on the **VO stem only**, padded to the picture length (EP22 reference balance against the +5.5 dB bed). **NEVER `volume=2.0` + `alimiter`** — that
   gain stage was for the quiet Higgsfield VESPER; the ElevenLabs clone is already hot and it
   crushes the limiter (EP26 came out at −13.4 LUFS, distorted). Reference build that sounds right:
   `episodes/ep22_blue_morpho_v2/build/stitch.sh`, or run `_pipeline/remaster_vo.sh <episode>`.
   **Never bake copyrighted music.**
   **Score bed + SFX (every video, added 2026-09-08):** after the VO-only master exists, run
   `bash "_pipeline/mix_audio.sh" episodes/<epNN_slug> "<shot>:<sfx>,..."`. It mixes ONE consistent
   track under the narration — the channel's own original awe pad `_pipeline/audio_kit/gnosis_score_bed.mp3`
   (a 4-section awe journey — Mystery → Ascent → Tension → Awe — built on the Interstellar cue's
   harmonic devices; see `_pipeline/audio_kit/README.md`). The tool time-stretches it to the episode
   and applies a **dynamics envelope that peaks where the reveal line begins** — quiet in the hook,
   lifting through the mechanism, dipping at the tension beat, swelling under the reveal. It is
   NEVER a flat hum. It also places subtle SFX at **-14 dB** at the START of a shot ONLY where the visual clearly
   earns it (`shimmer` for light/sparkle, `soft_whoosh` for a pull-back or reveal of scale, `swell` for
   the closing reveal, `tick` on a caption change if wanted). **Restraint rule: 2–4 SFX per video max,
   never one on every shot; if a shot doesn't obviously call for one, it gets music + narration only.**
   Never change the music mid-video and never cut between tracks — the bed runs start to finish.
   Note the SFX map in `EDIT_NOTES.md`. Then re-export the platform cuts from the mixed master.
   **Brand watermark (every video):** as the final compositing step on the master, overlay
   `_pipeline/brand/watermark.png` at the **TOP-LEFT, 44px in and 300px down** (Wilder 2026-09-13: at 44px from the top the phone status bar and the Shorts back-arrow row cover it; 300px clears both) —
   `-i _pipeline/brand/watermark.png` + `overlay=44:300` (it is already sized for 1080-wide and
   pre-set to ~55% opacity, so no scaling/alpha needed). Top-left is deliberate: the bottom and
   right are taken by the burned caption, the keyword label, and the Shorts UI buttons. All the
   platform cuts inherit it from the master.
7. **QC the render** — pull a frame from the middle of each segment OF THE FINISHED VIDEO, build a
   contact sheet, and look at it. Every caption must sit on a visual that depicts it. This is the
   most important gate in the pipeline and it must be checked on the render, not the stills.
8. **Exports** — master, platform cuts in `exports/{tiktok,reels,shorts,youtube}/`, a `<10MB` web
   version, and a ~9.5MB two-pass `fps=30` upload file for Shorts.
9. **Queue for YouTube (automatic)** — after the render QC passes and `YOUTUBE_SHORTS.md` is
   written, run:
   `node "/home/user/gnosis-lab/_pipeline/queue_youtube.mjs" --episode <epNN>`
   Confirm it printed `✓ queued → scheduled_posts <id>` and note the id in the summary. Ashborn OS
   uploads it to the Gnosis Lab channel within ~5 minutes (private until the Google API audit
   passes — mention that in the summary). If the script fails: record the exact error in
   `EDIT_NOTES.md` and move on — it is idempotent, so the next night's run can safely re-invoke it
   for this episode. Never work around a failure by posting some other way.
   **Instagram = WINNERS ONLY (Wilder 2026-10-04 — the horse episode flopped on IG).**
   Do NOT queue tonight's episode to Instagram. Every episode still gets YouTube; Instagram gets
   only the proven ones. In Step 0 of every run, after the analytics pull, promote winners:
   an episode qualifies when it has had **≥ 48 h on YouTube** and sits **at or above the
   channel median in BOTH views and retention %** in `_pipeline/analytics/latest.json`, and has
   no Instagram row yet. Promote at most **one** episode per run (the strongest), with
   `node "/home/user/gnosis-lab/_pipeline/queue_youtube.mjs" --platform instagram --episode <epNN> --date <today> --time 17:00`
   → confirm `✓ queued REEL → scheduled_posts <id>`. It reuses the YouTube upload and posts the
   `## Instagram Caption` block from `YOUTUBE_SHORTS.md` (derives one if missing). If
   `_pipeline/promote_to_instagram.mjs` exists, use it instead of choosing by hand. If nothing
   qualifies, promote nothing and say "nothing to promote" in the summary. If @thegnosis_lab is
   not connected the script says so — record it and move on. Never re-promote an episode Wilder
   removed from Instagram (listed under "Removed from Instagram" in `LEARNINGS.md`).

Caps per night: ~20 image jobs, ~18 video jobs. Kling is ~8.75 credits/clip; check `balance` first
and note credits used in the summary.

## Also build, but do NOT schedule
A ~15–18s teaser from the 5 strongest clips, same recipe, in `teaser_15s/`. It's a ready asset for
whenever publishing returns — just don't post it.

## Deliverables every run
Stage into `review/<date>_<slug>/`: `stills/ clips/ full_60s/ teaser_15s/` plus `timeline.json`,
`SCRIPT_60s.md`, `JOB_MAP.md`, the rendered QC contact sheet, and:
- **`captions.md`** — 3 title/caption variants (rule E5: always three).
- **`POST_READY.md`** — one paste-ready block (caption + CTA + hashtags) for manual TikTok/IG posting,
  plus CTA alternates. Standing tags: `#neuroscience #biology #humanbody #anatomy #learnontiktok
  #didyouknow #gnosislab` + topic tags. **Never `#ai`/`#aiart`/model names** — the edge is not
  reading as AI content.
- **`YOUTUBE_SHORTS.md`** — title (the hook goes in the TITLE on Shorts, not the description),
  description, and tags. **Use the EP17 file as the canonical format** — `queue_youtube.mjs`
  parses it: an `**Upload file:**` line with the path in backticks, then `## Title`,
  `## Description`, and `## Tags` sections each holding their content in a fenced code block
  (title ends with `#shorts`; tags are one comma-separated list). Do NOT write "do not upload
  yet" notes — uploading is automatic now.
  **Plus a `## Instagram Caption` fenced block (2026-09-13):** the hook line, the reveal sentence
  (name the subject), the same single `Source:` line, then exactly
  `Follow @thegnosis_lab — one mechanism, taken apart, most days.` and 5–6 hashtags. ≤ 500 chars
  before the hashtags. **Never the word "subscribe" on Instagram**; the ask is follow.
- **`SOURCES.md`** — 1–3 real primary/authoritative citations backing the episode's claims
  (journal + year). These also become the end-of-video source card and go in the description.
  Rigor is the channel's edge against "it's just AI" — always cite.
- **`EDIT_NOTES.md`** — what to watch for, the weakest shot and why, choices made without Wilder
  (rule E5), and any blockers.

Append the episode to `episode_log.json` and mark the topic built in `TOPIC_BANK.md`. In the
episode's log record, include a `hypothesis` field (the one variable you tested this run, from
Step 0.4) so next cycle's Analyst can score it, and add the row to the Hypothesis Ledger in
`LEARNINGS.md`.

## Community kit (added 2026-10-03 — text and existing assets only; steps 1–9 unchanged)

Write `COMMUNITY.md` in the episode folder after step 9. It costs no credits and changes nothing
about how the video is made. Wilder posts these by hand; stickers can't be added through the API.

1. **Pinned question comment** — one question about the mechanism that a viewer can answer from
   their own belief, e.g. "Did you think blue eyes had blue pigment?" Under 120 characters, no
   hashtags, no "follow". Use it on the Short now, and on the Reel if the episode is promoted.
2. **Story reshare** — the file to use is the `teaser_15s/` cut this run already builds (it stays
   unposted on TikTok as before). Give one hook line for the story text, under 60 characters,
   that does NOT name the subject (the reveal stays in the reel).
3. **Quiz sticker** — one true/false statement on the episode's mechanism, and the answer, taken
   from a claim already in `SOURCES.md`.
4. **Poll (only on runs where the date is a Monday or Thursday, LA time)** — "What should we take
   apart next?" with two options: the next two unbuilt GREEN topics in `TOPIC_BANK.md`, written as
   a 1–3 word name each. Wilder reports the winner by adding it to `_pipeline/PRIORITY_NEXT.md`;
   if that file exists, build its topic first and then delete the file.
5. **Behind the scenes (optional)** — if the stills contact sheet is clean, note its path as a
   BTS story asset with a one-line caption. Never the QC sheet with failed frames.

Add a "Community kit" line to the summary listing what's in `COMMUNITY.md`.

## Summary to Wilder
Topic built, runtime, shot count, credits used, the weakest shot and your recommendation, and
anything blocked. Report the YouTube queue result (scheduled_posts id, or the error if it failed).
TikTok/IG he still posts manually — TikTok natively if he wants a licensed sound (no scheduler can
attach one). **Also report the git push result** (commit hash, or the error).

---

## SUSPENDED — restore only when Wilder says publishing is fixed

**Phase 1 (deploy):** check `approved/`; for each item on https://app.omnisocials.com (Ashborn
Studios workspace): Create post → caption box → type caption+hashtags → image icon → "Upload media"
ONCE (mounts hidden file inputs) → find "file upload input" + `file_upload` with the video (<10MB;
else re-encode crf 24 aac 128k) → Upload → click the new thumbnail → "Add 1 video" → click the "..."
accounts chip and toggle ON only the intended channel → "Schedule Post" → hour/minute are DROPDOWNS
(click, scroll, click; typing fails); default 7:00 PM local → confirm the chip has a green ring →
Schedule Post → verify on /posts. Move to `deployed/`, log it.

**Phase 3 (teaser auto-schedule):** Wilder pre-approved teaser scheduling on 2026-07-22 — 7PM,
TikTok only, Instagram OFF. Full episodes and the 60s deep cut always await manual approval.
**⚠ Rebuild trap (2026-09-19):** `mix_audio.sh` takes its VIDEO from `masters/*_MASTER_VO_ONLY.mp4` and only creates that copy if it is missing. When you rebuild an episode (new clips) you MUST refresh or delete the `_VO_ONLY` file before mixing, or the old shots come back silently. `_pipeline/remaster_vo.sh` handles it; a hand stitch must `rm masters/*_VO_ONLY.mp4` first.
