# [YOUR CHANNEL NAME] — project rules for Claude Code

A faceless vertical-Shorts channel built from recorded gameplay. The core series is
"What happens if…?" experiments, but the channel posts **any** gameplay Short with viral potential
(see "Content formats" below).

> **Fill these in before your first run.** They are referenced throughout this file and the skill.
>
> | Placeholder | What to put | Neutral example |
> |---|---|---|
> | `[YOUR CHANNEL NAME]` | Channel name | "Game Lab" |
> | `[YOUR GAME]` | The game you record | "GTA VI", "Cyberpunk 2077" |
> | `[YOUR CAPTURE SOURCE]` | Console or PC capture | "PS5 share capture", "OBS on PC" |
> | `[YOUR BRAND COLOURS]` | 2–3 colours, one accent | "near-black background, one warm accent" |
> | `[YOUR CAPTION FONT]` | An installed heavy sans | "Anton", "Montserrat Black", "Oswald Heavy" |
> | `[YOUR CAPTION STYLE]` | How captions look | "white text, thick black outline, one accent-colour word per line" |
> | `[YOUR VOICE STYLE]` | Narrator direction | "neutral, conversational narrator, dry and understated" |
> | `[YOUR TAGLINE]` | Optional sign-off | leave blank if you don't want one |

## THE JOB (read this first)
When the user hands over gameplay, the job is: **find everything in the footage that can become a
viral Short, in any format, and make it.** Most recordings are normal play: missions, driving,
fights, crashes the player caused, crashes they witnessed, scenery, NPC behaviour, random chaos.
Every one of those is raw material.

- Do **not** judge footage against a shot list or a plan. A list is only a recording guide. Footage
  that matches nothing on it is still fully usable.
- Do **not** stop at the first pass or the first category. Catalogue **all** action and **all**
  beauty before ranking. If the user has to tell you about a crash, fight or interaction you
  missed, the analysis was too coarse — fix the method, not just that one moment.
- Story missions are usable gameplay. Only cutscenes, plot dialogue and big story reveals are
  off-limits.

### Links
- **Production playbook** (analysis, cutting, scripts, captions, ffmpeg recipes):
  `.claude/skills/gameplay-to-shorts/SKILL.md`. That file covers HOW; this file always wins on WHAT.
- Templates: `templates/script-template.md`, `templates/clip-log-template.md`

## Folder layout
- `clips/` — raw recordings. **ORIGINALS: never modify, move, rename or delete them.**
- `work/` — scratch area (proxies, contact sheets, audio scans, clip log, tools). Create if missing.
- `shorts/NN-slug/` — one folder per Short, holding `rough_cut.mp4`, `script.md`,
  `voice/` (drop generated voiceover files here), `captions.ass` and `final.mp4`.
- `templates/` — the clip-log and script formats.

## Content formats (all allowed, mix them)
- **What happens if…?** — a test and its result (the core series).
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

## Locked rules (do not reargue)
- Vertical 9:16, 1080×1920, **never under 30 s**. Don't pad with filler to reach 30 s; add a second
  clip, a ranking entry or a comparison instead.
- **Target 30–45 s for most formats.** On **dialogue-led Shorts there is no upper limit** — clarity
  wins. Never trim a sentence, a reaction or a hold just to hit a number.
- **Hook first.** 0–3 s is the strongest real moment from the same Short, with voiceover. Then
  setup → build → full payoff, optional replay, honest takeaway. Adapt the beats to the format
  (a ranking counts down; a showcase builds to the best shot).
- **The hook must PLAY the whole spoken sentence, not just caption it.** The clip runs to the end of
  the utterance plus a hold, so the viewer hears the speaker finish. A full caption over audio that
  cuts mid-sentence still reads as broken. Never truncate a hook line with "…" or a dash.
- **A "what happens if" Short opens on the what-if question**, never on a clip lifted from the
  middle or the end. The question is the hook.
- **Never cut away before a reaction has finished.** When the player causes something — a hit, an
  insult, trash talk — the reply plays out in full before the cut.
- **Never cut on the last syllable.** Hold roughly **0.55–0.85 s** of picture after a line ends,
  capped so it doesn't run into the next line. Cutting the instant someone stops talking looks
  rushed. Hooks are the one exception — they cut hard on purpose.
- The hook shot must come from the same Short. **Never fabricate, exaggerate or imply a reaction the
  footage doesn't show.** An honest "nothing happens" is allowed.
- **Record first, then script.** The voice is written only from what the footage shows.
- Keep game audio under the voice. No logo intro, no subscribe outro, no long intros.
- **Story-free:** no cutscenes, mission dialogue or plot. Mute or cut licensed radio and music
  (copyright-claim risk).
- **Never reuse the same source seconds in two Shorts.**
- Faceless, narrated by a synthetic or recorded voiceover that the user generates.

## Look and mix
- **Captions:** `[YOUR CAPTION STYLE]` — e.g. white text with a thick black outline and one
  accent-colour word per line. Font: `[YOUR CAPTION FONT]`.
  - **One fixed position in every video.** A headline at the top for the whole Short, and spoken
    lines always in the same lower slot (around y≈1330 on a 1920-tall frame).
  - **Small.** No stroked meme look, no per-line repositioning, no emojis.
  - Dialogue lines get a speaker tag (e.g. HER / HIM / ME); swearing is asterisked.
- **Colours:** `[YOUR BRAND COLOURS]`.
- **Counter tag** for repeated actions ("HIT #3", "TRY #5") in your accent colour. Good for
  carrying escalation without narration.
- **Mix:** the voice is never loud and **the game is never muted under it**. Voiceover about
  −21 LUFS, game ducked only about −5 dB under voice spans with ~120 ms ramps. Master to
  −14 LUFS, true peak ≤ −1.5 dBFS.
- **Dialogue-led Shorts:** the NPCs' lines are the script and are subtitled. Voiceover goes only in
  gaps where nobody is speaking and **never overlaps a spoken line**.
- Tagline (optional): `[YOUR TAGLINE]`.

## Honesty and rights
- Never claim a mechanic, reaction or outcome the footage doesn't show. Verify every claim at full
  resolution before writing it into a script or a title.
- Titles are direct and curiosity-led. Never overstate the result.
- Most publishers tolerate fan gameplay footage for **non-commercial** use. Avoid pre-release or
  leaked footage, endings, cutscene compilations, big plot reveals, isolated in-game music or TV,
  cheats and mods. Buying a game does not grant commercial rights — check the publisher's own
  policy before monetising.
- Ask before downloading anything (models, fonts, installers), even if it seems routine.

## Workflow
1. **ANALYSE** every clip densely and write `work/clip_log.md`: an event catalogue of every action
   and beauty moment (method in the skill, format in `templates/clip-log-template.md`).
2. **SELECT** — present a ranked list of candidate Shorts across **all** formats, aiming for as many
   viable Shorts as the footage supports, with a viral score and reasoning. **Wait for approval.**
3. **ROUGH CUT** approved Shorts from the ORIGINAL files, leaving room for the voice.
4. **SCRIPT** — write `script.md` per Short (timed VO lines, on-screen text, title, hook variants).
   Wait for the user's voiceover files.
5. **FINAL** — sync VO, duck game audio, word-timed captions, counter tags, replay, −14 LUFS.
   Export `final.mp4`.

## Working style
- Ask before anything destructive or irreversible. Show the ranked list before cutting.
- Plain-language summaries, short. Give real opinions and push back; safe answers aren't useful.
- Report what is weak or risky (music, story content, soft crop, uncertain speaker) rather than
  quietly shipping it.
