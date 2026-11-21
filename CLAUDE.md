# Gameplay → Shorts — project rules for Claude Code

Turns raw gameplay recordings into ready-to-post vertical Shorts. **No channel, branding or setup
form is needed.** The user drops in recordings; you find the moments worth posting, cut them, write
the voiceover script, and do the final edit once the user supplies the voice.

- **Production playbook** (analysis, cutting, scripts, captions, ffmpeg recipes):
  `.claude/skills/gameplay-to-shorts/SKILL.md`. That file covers HOW; this file always wins on WHAT.
- Templates: `templates/script-template.md`, `templates/clip-log-template.md`

## FIRST RUN — do this automatically

When the user opens this folder for the first time (no `work/clip_log.md` yet), or says anything like
"set this up", "start" or "help", run this flow. Don't wait for them to know the steps.

1. **Welcome, in two lines.** Say what the system does and that the first goal is **one finished
   sample Short**, not a batch.
2. **Check the tools.** ffmpeg (full build), Python 3 with `numpy`, `pillow` and `faster-whisper`,
   and a heavy caption font (playbook §0). List what's missing and **ask before installing
   anything**. Give the exact command for their system (Windows: winget, macOS: brew).
3. **Ask for the recordings.** "Put your raw gameplay recordings in the `clips` folder (or tell me
   where they are), then tell me when they're in." Then wait. Any game and any capture source works.
4. **Analyse everything** (playbook §1–2). While it runs, give short progress lines. Then show a
   plain summary: what's in the footage, and the **top 5 Short ideas** with one line each.
5. **Make ONE sample.** Recommend the strongest idea (or use the one the user picks) and build it
   fully: the 9:16 rough cut and `script.md` (playbook §4–5). Show the rough cut and the voice script
   as a numbered list of lines.
6. **Hand over the voice step.** Tell the user, plainly:
   - generate **each numbered line separately** in ElevenLabs (or record them),
   - download them and name them `01.mp3`, `02.mp3`… in line order,
   - put them in `shorts/01-<name>/voice/` (or attach them in the chat), then say "done".
7. **Final edit** (playbook §6): sync the voice, mix, captions, loudness, QC. Deliver `final.mp4` and
   show where it is.
8. **Ask what to fix.** "Watch it on your phone. Anything to change — crop, captions, pacing, voice
   level, hook?" Apply every fix, re-export, and **save each fix as a one-line rule in `preferences.md`**
   (create it if missing) so it sticks for every future Short.
9. **Only after the sample is approved, offer the batch:** "Want me to make the rest of the list in
   one go?" Then rough-cut and script all approved Shorts together, collect all the voice files at
   once, and finish them together.

Never jump straight to a batch on the first run. One good sample first, fixes second, volume third.

## Style defaults (no setup needed)

Use these unless the user asks for something else. Never block on them.

| Setting | Default |
|---|---|
| Captions | White text, thick black outline, one yellow accent word per chunk |
| Caption font | A heavy sans already installed (Anton, Montserrat Black, Oswald, Impact, Arial Black — in that order). Ask before installing a new one |
| Voice style | Neutral, conversational narrator — dry and understated, like a friend telling you what they just saw |
| Accent colour | Yellow `#FFD000` |
| Sign-off | None |

If the user gives a channel name, colours, font or voice style at any point, use them and record
them in `preferences.md`.

**Read `preferences.md` at the start of every session.** It holds this user's fixes and choices and
always wins over the defaults. Never edit this file (CLAUDE.md) to store preferences — updates
replace it.

## UPDATING THE SYSTEM

When the user says "update", "update the system" or similar:
1. If this folder is a git repository, run `git pull`.
2. If it isn't (the user downloaded the ZIP), ask before downloading, then fetch the latest version
   from https://github.com/nickshana-dev/gta6-shorts-system (a `git clone` into a temporary folder
   is fine; install git first only if the user agrees) and copy over **only** the system files:
   `CLAUDE.md`, `README.md`, `LICENSE`, `.gitignore`, `.claude/skills/`, `templates/` and
   `gameplay-to-shorts-SKILL.md`.
3. **Never touch** `clips/`, `work/`, `shorts/` or `preferences.md`.
4. Tell the user in one or two lines what changed (read the new README or the commit messages).
Nothing needs reinstalling — ffmpeg, Python and fonts stay as they are.

## THE JOB
When the user hands over gameplay, the job is: **find everything in the footage that can become a
viral Short, in any format, and make it.** Most recordings are normal play: missions, driving,
fights, crashes the player caused, crashes they witnessed, scenery, NPC behaviour, random chaos.
Every one of those is raw material.

- Do **not** judge footage against a shot list or a plan. Footage that matches nothing on a list is
  still fully usable.
- Do **not** stop at the first pass or the first category. Catalogue **all** action and **all**
  beauty before ranking. If the user has to tell you about a crash, fight or interaction you
  missed, the analysis was too coarse — fix the method, not just that one moment.
- Story missions are usable gameplay. Only cutscenes, plot dialogue and big story reveals are
  off-limits.

## Folder layout
- `clips/` — raw recordings. **ORIGINALS: never modify, move, rename or delete them.**
- `work/` — scratch area (proxies, contact sheets, audio scans, clip log, tools). Create if missing.
- `shorts/NN-slug/` — one folder per Short, holding `rough_cut.mp4`, `script.md`,
  `voice/` (the user's voiceover files), `captions.ass` and `final.mp4`.
- `templates/` — the clip-log and script formats.

## Content formats (all allowed, mix them)
- **What happens if…?** — a test and its result.
- **Rankings** — "Best / worst / craziest / most brutal…": crashes, fights, NPC reactions, cars,
  police responses. Countdown 5→1 with the best last.
- **Moments / chaos** — one wild clip carried by hook, replay and narration.
- **NPC behaviour** — what NPCs do on their own: witnessed crashes, arguments, driving fails,
  reactions, overheard dialogue.
- **Showcase / beauty** — how the game looks: sunsets, underwater, city at night, weather, small
  realism details.
- **Detail / realism** — "they actually animated this…": physics, damage, animations, reflections.
- **Compilations with a frame** — "every crash in my first hour", "I did X to five different people".
- **Comparisons** — day vs night, slow vs fast, this NPC vs that NPC.

If footage fits a strong format not listed here, use it.

## Locked rules
- Vertical 9:16, 1080×1920, **never under 30 s**. Don't pad with filler to reach 30 s; add a second
  clip, a ranking entry or a comparison instead.
- **Target 30–45 s for most formats.** On **dialogue-led Shorts there is no upper limit** — clarity
  wins. Never trim a sentence, a reaction or a hold just to hit a number.
- **Hook first.** 0–3 s is the strongest real moment from the same Short, with voiceover. Then
  setup → build → full payoff, optional replay, honest takeaway. Adapt the beats to the format.
- **The hook must PLAY the whole spoken sentence, not just caption it.** Never truncate a hook line
  with "…" or a dash.
- **A "what happens if" Short opens on the what-if question.** The question is the hook.
- **Never cut away before a reaction has finished.**
- **Never cut on the last syllable.** Hold roughly **0.55–0.85 s** of picture after a line ends.
  Hooks are the one exception — they cut hard on purpose.
- **Never fabricate, exaggerate or imply a reaction the footage doesn't show.** An honest
  "nothing happens" is allowed.
- **Footage first, then script.** The voice is written only from what the footage shows.
- Keep game audio under the voice. No logo intro, no subscribe outro, no long intros.
- **Story-free:** no cutscenes, mission dialogue or plot. Mute or cut licensed radio and music
  (copyright-claim risk).
- **Never reuse the same source seconds in two Shorts.**

## Look and mix
- **Captions:** per the style defaults (or the user's preferences).
  - **One fixed position in every video.** A headline at the top for the whole Short, and spoken
    lines always in the same lower slot (around y≈1330 on a 1920-tall frame).
  - **Small.** No stroked meme look, no per-line repositioning, no emojis.
  - Dialogue lines get a speaker tag (e.g. HER / HIM / ME); swearing is asterisked.
- **Counter tag** for repeated actions ("HIT #3", "TRY #5") in the accent colour.
- **Mix:** the voice is never loud and **the game is never muted under it**. Voiceover about
  −21 LUFS, game ducked only about −5 dB under voice spans with ~120 ms ramps. Master to
  −14 LUFS, true peak ≤ −1.5 dBFS.
- **Dialogue-led Shorts:** the NPCs' lines are the script and are subtitled. Voiceover goes only in
  gaps where nobody is speaking and **never overlaps a spoken line**.

## Honesty and rights
- Never claim a mechanic, reaction or outcome the footage doesn't show. Verify every claim at full
  resolution before writing it into a script or a title.
- Titles are direct and curiosity-led. Never overstate the result.
- Most publishers tolerate fan gameplay footage for **non-commercial** use. Avoid pre-release or
  leaked footage, endings, cutscene compilations, big plot reveals, isolated in-game music or TV,
  cheats and mods. Buying a game does not grant commercial rights — check the publisher's own
  policy before monetising.
- Ask before downloading anything (models, fonts, installers), even if it seems routine.

## Workflow after the first run
1. **ANALYSE** new clips densely and update `work/clip_log.md` (method in the skill).
2. **SELECT** — a ranked list of candidate Shorts across **all** formats, with a viral score and
   reasoning. **Wait for approval.**
3. **ROUGH CUT** approved Shorts from the ORIGINAL files, leaving room for the voice.
4. **SCRIPT** — `script.md` per Short with numbered voice lines. Collect all voice files at once.
5. **FINAL** — sync voice, mix, captions, counter tags, replay, −14 LUFS. Export `final.mp4`.

## Working style
- The user may not be technical. Plain language, short messages, one clear next step at a time.
- Ask before anything destructive or irreversible. Show the ranked list before cutting.
- Report what is weak or risky (music, story content, soft crop, uncertain speaker) rather than
  quietly shipping it.
