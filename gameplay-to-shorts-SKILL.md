---
name: gameplay-to-shorts
description: Turns raw gameplay recordings into ready-to-post vertical Shorts — finds the best moments, cuts 9:16, writes the voiceover script, and does the final edit with captions once the user supplies the voice. Use when someone shares gameplay footage or wants Shorts made from it.
---

# Gameplay → Shorts

Standalone version: everything the system needs is in this one file. It works best in **Claude Code**
(the Code tab of the Claude desktop app, or the CLI), opened on a folder that holds the recordings,
because the work needs ffmpeg and Python on the user's computer and console recordings are large.
This file is a snapshot. The latest version is at https://github.com/nickshana-dev/gta6-shorts-system
— if the user asks to update, tell them to download this file again from the same link (or switch
to the GitHub version, which updates itself with "update the system").

Save the user's fixes and preferences as one-line rules in `preferences.md` in the working folder,
and read that file at the start of every session.

# Part 1 — What to make, and the first run
Turns raw gameplay recordings into ready-to-post vertical Shorts. **No channel, branding or setup
form is needed.** The user drops in recordings; you find the moments worth posting, cut them, write
the voiceover script, and do the final edit once the user supplies the voice.

- **Part 1** (this part) covers WHAT to make and the first-run flow. **Part 2** is the production
  playbook (HOW). The templates are in the appendices. Part 1 always wins.

## FIRST RUN — do this automatically

As soon as this file is loaded — or when the user says anything like "set this up", "start" or
"help" — run this flow. Don't wait for them to know the steps.

1. **Welcome, in two lines.** Say what the system does and that the first goal is **one finished
   sample Short**, not a batch.
2. **Check the tools.** ffmpeg (full build), Python 3 with `numpy`, `pillow` and `faster-whisper`,
   and a heavy caption font (Part 2 §0). List what's missing and **ask before installing
   anything**. Give the exact command for their system (Windows: winget, macOS: brew).
3. **Ask for the recordings.** "Put your raw gameplay recordings in the `clips` folder (or tell me
   where they are), then tell me when they're in." Then wait. Any game and any capture source works.
4. **Analyse everything** (Part 2 §1–2). While it runs, give short progress lines. Then show a
   plain summary: what's in the footage, and the **top 5 Short ideas** with one line each.
5. **Make ONE sample.** Recommend the strongest idea (or use the one the user picks) and build it
   fully: the 9:16 rough cut and `script.md` (Part 2 §4–5). Show the rough cut and the voice script
   as a numbered list of lines.
6. **Hand over the voice step.** Tell the user, plainly:
   - generate **each numbered line separately** in ElevenLabs (or record them),
   - download them and name them `01.mp3`, `02.mp3`… in line order,
   - put them in `shorts/01-<name>/voice/` (or attach them in the chat), then say "done".
7. **Final edit** (Part 2 §6): sync the voice, mix, captions, loudness, QC. Deliver `final.mp4` and
   show where it is.
8. **Ask what to fix.** "Watch it on your phone. Anything to change — crop, captions, pacing, voice
   level, hook?" Apply every fix, re-export, and **save each fix as a one-line rule in a `preferences.md`
   file in the working folder** so it sticks for every future Short. Read that file at the start of
   every session.
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
1. **ANALYSE** new clips densely and update `work/clip_log.md` (method in Part 2).
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

# Part 2 — Production playbook
# Gameplay → Shorts: production playbook

Part 1 always wins. This part covers HOW.

Work in the user's current folder. Create `clips/`, `work/` and `shorts/` there if they don't exist.
Raw recordings go in `clips/`, scratch in `work/`, output in `shorts/NN-slug/`.

## 0. Setup checks

**ffmpeg/ffprobe on PATH?** You need a full build (with `libass`, `zimg`/zscale and `libvmaf`).

```
# Windows
winget install --id Gyan.FFmpeg --accept-source-agreements --accept-package-agreements

# macOS
brew install ffmpeg
```

Restart the shell afterwards and confirm with `ffmpeg -version` — check the configuration line
contains `--enable-libass` and `--enable-libzimg`.

**Python 3** with `numpy`, `pillow`, and `faster-whisper` (needed for caption timing and for
transcribing in-game dialogue):

```
pip install numpy pillow faster-whisper
```

`faster-whisper` uses CTranslate2, so **torch is not required** and it runs fine on CPU.
Pre-download the model so the final pass doesn't stall:

```
python -c "from faster_whisper import WhisperModel; WhisperModel('base.en', device='cpu', compute_type='int8')"
```

**Fonts:** check that the caption font (Part 1 style defaults) is installed (Windows: `C:\Windows\Fonts` and
`%LOCALAPPDATA%\Microsoft\Windows\Fonts`; macOS: `/Library/Fonts` and `~/Library/Fonts`).
If it isn't, **ask which font to install** — don't silently fall back to Arial.

> Gotcha: on Windows, `Get-ChildItem -Include *name*` returns nothing without `-Recurse`. That has
> produced a false "no fonts installed" result before.

**Paths contain spaces:** always quote them.

**Check the recordings copied correctly** before trusting them. A failed transfer from a console
often leaves files that are the right size but filled with `0xFF` or zero bytes. Byte-scan each
file for long uniform runs and probe it with ffprobe; a file that fails `ffprobe` or is mostly
uniform cannot be recovered — it has to be re-copied from the source device.

## 1. Probe every clip first

```
ffprobe -v error -show_entries format=duration:stream=index,codec_type,codec_name,width,height,r_frame_rate,pix_fmt,color_transfer,color_primaries,channels -of json "<clip>"
```

Record resolution, fps, codec and HDR status.

- **Coded vs display size:** some encoders pad (e.g. coded 1920×1088 decoding to 1920×1080).
  ffmpeg crops this automatically — confirm by decoding one frame.
- **HDR:** if `color_transfer` is `smpte2084` or `arib-std-b67` the footage is HDR. **Every frame
  grab and export must be tonemapped to SDR** or it will look washed out:
  ```
  zscale=t=linear:npl=203,format=gbrpf32le,zscale=p=bt709,tonemap=tonemap=mobius:desat=0,zscale=t=bt709:m=bt709:r=tv,format=yuv420p
  ```
  Tested alternatives that look worse: `tonemap=hable` goes grey and flat; `npl=100` blows out the
  sky. Tune `npl` if your capture differs.
- **Licensed music:** if the game has a radio or licensed soundtrack, check whether it is audible
  before planning any Short around that audio. A reliable test is an onset-envelope autocorrelation
  over a few sections: a clear peak in the 60–180 BPM band means music is present. If there is
  music, mute or replace that audio.
- VP9/AV1 decoding is slow. Build proxies once and analyse from them. **Cut finals from the
  originals.**
- A single ffmpeg decode often uses only a fraction of available cores. Running **3 clips in
  parallel** is typically ~3× faster than one at a time.

## 2. Analyse: catalogue EVERYTHING, densely

Goal: a complete event catalogue of the footage. **Action happens in 1–3 s bursts**, so sparse
sampling (every 10–20 s, or even every 2 s on its own) WILL miss crashes, punches and fights. Use
several detectors and union their results.

For each clip, in `work/<clipname>/`:

1. **Proxy** — `-vf "scale=-2:360,fps=10" -c:v libx264 -preset veryfast -crf 30 -c:a aac -b:a 96k
   proxy.mp4` (add the tonemap first if HDR).
2. **Overview sheets** — one frame per second (`fps=1`), tiled with burned timestamps, to see what
   each stretch of the clip is (driving, on foot, mission, menu, swimming…).
3. **Audio transients** — mono 16 kHz wav → short-window RMS; flag onsets ≥ ~8–11 dB over a rolling
   median. Catches impacts, crashes, gunshots, punches, horns, shouts, sirens, glass, explosions.
4. **Visual events** — scene-change/motion scores (`select='gt(scene,0.15)'` with `showinfo`, or
   frame-difference magnitude per 0.2 s from the proxy). Catches camera shake, sudden motion,
   ragdolls and wrecks that make little noise.
5. **HUD/state cues** — wanted level appearing, health drops, death/arrest screens, combat prompts,
   vehicle entry/exit, tooltips. Spot-check frames for these. **In-game tooltips often reveal
   mechanics nobody has noticed** and make excellent Shorts on their own.
6. **Speech** — run faster-whisper over the game audio for NPC lines. Real NPC dialogue is gold for
   hooks and can carry an entire Short.
7. **For EVERY flagged window**, pull frames at 5–10 fps for ±4 s and look at them yourself.
   Classify what actually happened. **Never classify from a single frame.**
8. **Beauty pass** — rate stretches for visual quality (light, weather, water, skyline, sunset,
   night city, underwater, interiors) and note which survive a clean 9:16 crop without HUD.

Write `work/clip_log.md` as an event catalogue — format in Appendix A.

Categories: `crash-player` · `crash-witnessed` · `fight` · `police/wanted` · `shooting/explosion` ·
`NPC-reaction` · `NPC-behaviour` · `driving-stunt/fail` · `physics/damage` · `funny/glitch` ·
`beauty/scenery` · `detail/realism` · `what-if-test` · `other`.

Then add a summary: counts per category, the 10 strongest moments overall, and problems (licensed
music, burned-in subtitles, cutscenes, menus, anything to avoid).

**Coverage check before moving on:** every audio onset and every visual spike must be either
catalogued or explicitly dismissed (menu, cutscene, nothing). If the user mentions something you
didn't catalogue, your detection was wrong — fix the method, don't just add that one moment.

## 3. Pick Shorts and score them

Score each candidate 1–5 on each axis, then rank by total:

- **Question clarity** — is it understood in one line without knowing the game?
- **Payoff strength** — is the result visible, surprising, funny or satisfying?
- **Hook frame** — is there a 1–2 s moment that makes a thumb stop?
- **Escalation** — does it build (counter, repeats, crowd growing)?
- **Loopability** — can the end flow back into the start?
- **Search/timing** — is it something people are actively searching for right now?

Also look for ones the edit and narration can rescue: a weak single attempt plus a strong second
subject, a deadpan "nothing happened" with a good narration angle, or a comparison (day vs night,
slow vs fast). **Say plainly which are carried by footage and which by edit.**

Present a table: rank, working title, source clip + timestamps, total score, one-line reason,
risks. **Wait for approval before cutting.**

## 4. Rough cut

- Cut from the **ORIGINAL** file. Use accurate seeking so cuts land on frames.
- Reframe 16:9 → 9:16:
  - 1080p source: `crop=608:1080:X:0,scale=1080:1920:flags=lanczos` (soft but fine for Shorts).
  - 4K source: `crop=1216:2160:X:0,scale=1080:1920:flags=lanczos` (sharp).
  - **Measure X by rendering candidate crops, not by eye.** Render the same frame at several X
    values side by side and pick. Guessing from a small contact sheet has put the subject
    off-frame for an entire Short.
  - If the subject moves, animate X across the segment (piecewise-linear keyframes).
    **Never let the payoff action leave the frame.**
  - Wide action that can't survive a crop (big crash, traffic jam): full 16:9 frame scaled to
    1080 wide, centred, over a blurred and darkened 9:16 fill of the same footage. Use sparingly.
- **HUD and burned-in text.** A centre crop already excludes most corner HUD (minimap, prompts,
  health, wanted level). Only the *vertical* crop removes burned-in subtitles. **Measure where they
  sit** on your capture — find the pixel rows the text occupies, then crop above them:
  - Keep the full height (`crop=608:1080`) where there is no burned-in text — this is sharpest.
  - Where subtitles appear, shorten the crop (e.g. `crop=532:945:X:0`) so the text is cut off.
    Dialogue subtitles often sit *higher* than objective/mission text, so measure both.
  - Upper-left tooltips need the opposite: a left-biased crop (e.g. `crop=495:880:20:0`) that keeps
    the tooltip box and clears the minimap. A sharp left-biased crop beats a blurred-fill composite.
- **Shorts UI safe zone:** keep faces, payoff action and text out of the bottom ~380 px
  (title/description) and the right ~160 px (buttons). Captions sit roughly y=1000–1350.
- **Structure:** hook 0–3 s → setup → build → full payoff → optional 0.5× or zoomed replay →
  takeaway.
- **Hook rules** (these were learned the hard way):
  - The hook must **play the whole spoken sentence**, then hold. A full caption over audio that
    cuts mid-sentence reads as broken.
  - A **what-if** Short opens on the question, not a clip lifted from later.
  - Where the hook plays a line in full, **delete the later in-context replay** of that same line —
    it is a straight duplicate and usually makes the Short shorter.
  - A weak hook is a rebuild, not a tweak. Two short lines that escalate beat one line alone.
- **Hold after every line.** Never cut on the last syllable: leave **~0.55–0.85 s** of picture after
  a line ends, capped so it doesn't run into the next line. Check every segment's tail gap
  programmatically; cutting 0.1 s after the last word looks rushed, and it is easy to do this on
  every cut without noticing.
- **Never cut away before a reaction finishes.** List, per segment, any dialogue that starts just
  after the out point — that is the reply the viewer never hears.
- **Avoid menus and dead frames.** Pause screens, map screens, weapon wheels and transitions are
  often a grey or black flash. Scan the finished cut for near-uniform frames rather than trusting
  your eye.
- Remove licensed radio/music. Cut it, or replace that section's audio with ambience from elsewhere
  in the same clip.
- **Rough-cut export:** `-c:v libx264 -preset veryfast -crf 18 -pix_fmt yuv420p -r 30
  -c:a aac -b:a 192k -ar 48000 -movflags +faststart`. Use 60 fps if the source is 60 and the action
  is fast. Stay consistent per Short.
- Burn a small timecode in the corner of the **rough cut only** — it helps time the voice. Never in
  the final.

## 5. Voice script (`shorts/NN-slug/script.md`)

Write only what the footage shows. Format in Appendix B.

**Voice direction:** the voice style in Part 1 — by default a neutral, conversational narrator, dry and
understated, like a friend telling you what they just saw. Not a trailer announcer, not a tutorial.
Slightly faster than default, with a real pause after the hook line.

Number every voice line. Ask the user to generate **each line separately** (2–3 takes if they like) and name the files `01.mp3`, `02.mp3`… in line order, so each can be timed to its cut. Leave gaps so key
game sounds are heard clean. Aim for **~2.3–2.6 words per second of narrated time** — roughly
60–80 words per 35 s Short. On dialogue-led Shorts the voiceover is much lighter: it only fills
gaps where nobody is speaking.

**Hook patterns** (use only if the footage backs them):
- Consequence tease — "Attempt number seven was a mistake."
- Deadpan null — "I did this twenty times. He never looked up."
- Disbelief — "I didn't think this game would actually do that."
- Count/escalation — "Every time I did it, he got angrier."

**Loop trick:** write the last line so it runs into the first, and make the last shot a *different*
subject from the first so the eye doesn't register a repeat. A sentence that completes across the
loop point reads as one continuing thought rather than a restart.

**Counter tag:** for repeated actions, show "#1, #2…" as each one happens. It carries escalation
without narration.

## 6. Final edit (after `voice/` has audio)

1. **Transcribe each voice file** with faster-whisper (`word_timestamps=True`) for exact word
   timings.
   > **Whisper hallucinates on trailing silence.** Check word timings before trusting a transcript:
   > a run of words with zero or near-zero duration crammed into a fraction of a second (often
   > "…and I'll see you in the next video") is not in your audio. Scope the line to the real words.
   > Transcripts also mis-hear. Re-transcribe each used range on its own and cross-check against
   > the full-clip pass; where the two disagree, leave the line **uncaptioned** rather than guess.
2. **Place the lines** per the script. Nudge cuts so lines land on picture. If a take runs long,
   **move the cut rather than time-stretching the voice.**
3. **Audio:** the game is **never muted** under the voice. Voiceover about −21 LUFS, game ducked
   only ~−5 dB under voice spans with ~120 ms ramps. On dialogue-led Shorts the voiceover goes only
   in gaps and **never overlaps a spoken line** — assert this in code rather than checking by ear.
4. **Captions** — style and font from Part 1 (defaults or the user's preferences):
   - **Fixed positions in every video.** A headline at the top for the whole Short, every spoken
     line in the same lower slot (y≈1330).
   - **Small.** No stroked meme text, no per-line repositioning, no emojis.
   - 1–3 words per chunk, popping on per word group, with at most one accent-colour word per chunk.
   - Dialogue lines get a speaker tag; swearing is asterisked.
   - **Check who is speaking before tagging or titling.** Median pitch per line separates most
     voices (roughly < 160 Hz male, > 175 Hz female); mixed or very short lines are unreliable —
     say so rather than guessing. Whether "she" or "he" said something changes the title.
5. **Extras, restrained:** counter tag, a 1.15–1.3× punch-in or 0.5× replay at the payoff, a short
   impact sound only where the cut needs it. No glow, shake spam or meme overlays.
6. **Loudness:** master to `I=-14`, `TP=-1.5`, `LRA=11`, two-pass.
   > **Verify the result; don't trust the filter.** `loudnorm` with `linear=true` silently reverts
   > to dynamic mode when the required gain would breach the true-peak ceiling, and its true-peak
   > limiting overshoots — that has shipped a clipping master at +0.8 dBFS and a 1.4 dB-quiet one.
   > Measure the finished file and, if it's out, apply a flat gain plus a hard limiter and iterate
   > until both targets are met. If you use `alimiter`, set `level=disabled` (its auto-level
   > defaults to on and will push peaks back to full scale) and `attack=1` (the 5 ms default lets
   > transients through once the input is hot).
7. **Export** `final.mp4` at 1080×1920, same codec settings as the rough cut, **no timecode**.
8. **Always QC before sending:** scan for blank/near-uniform frames, read a 2 fps contact sheet of
   the whole Short, check the first frame (it is the default thumbnail), the duration and the safe
   zones. Watch it once end to end. Low-contrast shots (underwater, a plain wall) will trip a blank
   detector — look before acting on a flag.
9. Write the title, a 1–2 line description and 3–5 hashtags into `script.md`.

## 7. Report back

Keep it short: what was made, where it is, anything weak or risky (music, story content, soft crop,
an uncertain speaker, a claim you couldn't verify), and the next step. Report problems rather than
quietly shipping them.

## 8. Lessons — real mistakes, don't repeat them

1. **Don't judge footage against a list.** Catalogue everything that's there.
2. **Sparse sampling misses action.** Use audio transients plus dense frame checks.
3. **Always QC the finished file** with a blank-frame scan and a contact sheet. That is what catches
   menu flashes, burned-in subtitles and an off-frame speaker.
4. **Verify every claim at full resolution.** Things that turned out false on inspection: a
   "shipwreck" that was a reef wall, "rain" that was sun glare on dry tarmac, a "carjacking" that
   wasn't, a "drowning" that was a dive. Check the frames before writing the line.
5. **Who's speaking matters.** Check before tagging or titling.
6. **Transcripts mis-hear and drop words.** Re-transcribe each used range and cross-check.
7. **Showing a mechanic's text is not a video.** Pair every reveal with the footage that caused it,
   or it's a slideshow.
8. **Measure crops by rendering them.** Eyeballing a contact sheet puts subjects off-frame.
9. **Ask before downloading anything** — models, fonts, installers.

# Appendix A — Clip log template
# Clip log — event catalogue

Copy this into `work/clip_log.md` and fill it in from the dense analysis pass
(playbook §2). One section per source clip.

**Method line** — state what you actually ran, so the coverage can be checked later. For example:
> Analysed <date>. 10 fps proxies + 1 fps overview sheets + audio transient detection
> (onset ≥ 8 dB over a rolling median) + scene-change scores, with every flagged window verified
> visually at 5–10 fps.

**Specs line** — per clip: container/codec, coded vs display resolution, fps, SDR or HDR
(and the tonemap used), audio format, bitrate.

---

## <clip file name> — <duration>, <resolution>, <fps>, HDR yes/no

| In–Out | Category | What happens (only what is visible/audible) | Strength 1–5 | Crop OK? | Notes |
|---|---|---|---|---|---|
| 00:25–00:55 | crash-player | Example: vehicle leaves the road and rolls | 5 | y | hook candidate |
| 01:40–01:55 | menu | Pause/map screen | – | n | avoid, grey transition at 01:53 |

**Categories:** `crash-player` · `crash-witnessed` · `fight` · `police/wanted` ·
`shooting/explosion` · `NPC-reaction` · `NPC-behaviour` · `driving-stunt/fail` · `physics/damage` ·
`funny/glitch` · `beauty/scenery` · `detail/realism` · `what-if-test` · `menu` · `story` · `other`

**Crop OK?** — does the moment survive a clean 9:16 crop with no HUD or burned-in text?

Per clip, close with:
- **Payoff moments:** <timestamps>
- **Hook candidates:** <timestamps>
- **Problems:** licensed music, burned-in subtitles, cutscenes, menus, anything to avoid

---

## Summary

**Counts per category:** e.g. crash-player 6 · fight 1 · beauty 8 · detail 9 · avoid 2

**The 10 strongest moments**
1. `<clip>` 00:00–00:00 — one line on what it is
2. …

**Vehicles / locations / characters used** — useful for spotting variety and for the
"never reuse the same source seconds" rule.

**Problems that apply to everything**
- Licensed music present? (state how you checked)
- Burned-in text: which pixel rows, so the crop can clear it
- Menus, transitions and dead frames to avoid, with timestamps
- Anything off-limits (cutscenes, plot reveals, content you won't show)

**Coverage check** — confirm every audio onset and visual spike is either catalogued above or
explicitly dismissed. If something was missed, say what the detection method got wrong.

# Appendix B — Script template
# <Title>

Source: `<clip file>` · Range `<in>–<out>` · **Target length `<s>`**
One line on what this Short is and why it works.

> Write only what the footage shows. If you can't verify a claim at full resolution, don't write it.

## Beat sheet

| # | Out (timeline) | Source in | Picture | VO line | On-screen |
|---|---|---|---|---|---|
| 1 | 0:00–0:03 | 00:00 | **HOOK** — the strongest real moment. Plays the whole spoken sentence, then holds | "…" | — |
| 2 | 0:03–0:09 | 00:00 | Setup | "…" | — |
| 3 | 0:09–0:20 | 00:00 | Build | *(silence — let the game audio carry it)* | COUNTER #1 |
| 4 | 0:20–0:30 | 00:00 | Full payoff | "…" | — |
| 5 | 0:30–0:35 | 00:00 | Optional replay / takeaway | "…" | — |

Rules this table has to satisfy:
- The hook **plays the speaker finishing the sentence** — never truncate with "…" or a dash.
- A what-if Short opens on the **question**.
- Every cut holds **~0.55–0.85 s** after the last word (hooks excepted — they cut hard).
- No cut lands before a reaction has finished.
- No source seconds reused from another Short.

## The loop
How the last line runs into the first, and why the final shot doesn't read as a repeat of the
opening (different subject, different framing).

## Hook variants
1. "…"  ← recommended, and why
2. "…"
3. "…"

## Title options
1. **…**
2. …
3. …

## Description
One or two plain lines. Never overstate the result.

`#Hashtag1 #Hashtag2 #Shorts #…`

## Notes for the voice
Voice style from Part 1. Number every line (01, 02…) — the user generates each one as its own file. Word count and target duration (aim ~2.3–2.6 words per second of narrated
time). Mark deliberate silences — they are part of the edit, not gaps to fill. Call out any line
whose delivery matters (a rising pitch that completes into the next line, a throwaway last line).

## Edit notes
- Crop used per beat (`crop=W:H:X:0`), and why — especially where a shorter crop clears burned-in
  subtitles or a left-biased crop keeps a tooltip.
- Anything muted or replaced (licensed music, character dialogue).
- Menus, transitions or dead frames avoided, with source timestamps.
- Anything changed from the original plan, and why — so the next person doesn't undo it.
