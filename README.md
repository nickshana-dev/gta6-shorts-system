# gta6-shorts-system

Turns raw gameplay recordings into ready-to-post vertical Shorts.

You give it your recordings. It finds the moments worth posting, cuts them to 9:16, writes the
voiceover script, and — once you've generated the voice — does the final edit with captions and a
proper audio mix. It runs inside [Claude Code](https://claude.com/claude-code). No channel, editing
skills or setup form needed.

Built for GTA VI, but nothing in it is game-specific — it works with any gameplay recording, from
console or PC.

## Get it — two ways

**Option 1 — let Claude install it (recommended, and it can update itself)**
1. Open the **Claude desktop app** → **Code** tab, and open an empty folder.
2. Paste this:
   ```
   Install the system from https://github.com/nickshana-dev/gta6-shorts-system into this folder with git, then read its CLAUDE.md and start.
   ```
3. It downloads everything, checks your computer, and walks you through the rest.

(Prefer to do it yourself? `git clone https://github.com/nickshana-dev/gta6-shorts-system.git`, or
**Code** → **Download ZIP**, then open the folder in Claude Code and type **"start"**.)

**Option 2 — the single skill file**
Download [`gameplay-to-shorts-SKILL.md`](gameplay-to-shorts-SKILL.md) — the whole system in one
file. Open any folder in Claude Code, attach the file, and type **"start"**. This version doesn't
update itself; download it again for a new version.

**Updates:** this is the first version, and I'm improving it. To get the latest, open the folder
in Claude Code and type **"update the system"**. It pulls the new version and keeps your clips,
Shorts and saved preferences. Nothing gets reinstalled. Click **Watch** on this page to be told
when it changes.

You'll need a paid Claude plan (Pro or higher), which includes Claude Code. For the voice,
ElevenLabs works well, or record it yourself.

## How it works

**1. Setup.** On the first run it checks your computer for the tools it uses (ffmpeg, Python and a
couple of packages, a caption font). It tells you what's missing and asks before installing
anything.

**2. Your recordings.** It asks you to put your raw gameplay in the `clips` folder. Don't trim or
edit them — normal play is fine. Missions, driving, fights, crashes, scenery: all of it is useful.

**3. Analysis.** It goes through every recording — sounds, movement, NPC speech, on-screen cues — and
logs every moment worth posting. Then it shows you the top Short ideas.

**4. One sample first.** It builds **one** Short from the strongest idea and shows you the rough cut
and a numbered voice script.

**5. The voice.** Generate each numbered line separately in ElevenLabs (or record it), name the files
`01.mp3`, `02.mp3`… in order, drop them in the Short's `voice` folder, and say "done".

**6. Final edit.** It syncs the voice, mixes the game audio underneath, adds captions and exports
`final.mp4`.

**7. Fix, then scale.** Watch the sample on your phone and tell it what to change — crop, captions,
pacing, voice level, hook. It fixes it and remembers the fix for every future Short. **Only once the
sample is right**, ask it to make the rest of the list in one go.

> **Tip:** get one output you're happy with before generating more. Every fix you make on the first
> Short is applied to all the others automatically.

## What it does under the hood

- **Probes** every clip: resolution, fps, codec, HDR, and whether the recording copied correctly.
- **Analyses densely** — audio transient detection, scene-change scores, HUD/state cues and speech
  transcription, then verifies every flagged moment on screen.
- **Catalogues** everything into an event log: crashes, fights, NPC behaviour, physics, scenery.
- **Ranks** candidate Shorts with a viral score across formats: what-if tests, rankings, NPC
  moments, showcases, comparisons.
- **Cuts** 9:16 from the originals, keeping the subject framed and the HUD and burned-in subtitles
  out.
- **Writes** a timed voiceover script from what the footage actually shows.
- **Assembles** the final: voice synced to picture, game audio ducked (never muted), word-timed
  captions, mastered to −14 LUFS.

## Folder structure

```
CLAUDE.md                                   the rules, first-run flow and update command
preferences.md                              your saved fixes (created on first use, never overwritten)
.claude/skills/gameplay-to-shorts/SKILL.md  the production playbook (the HOW)
gameplay-to-shorts-SKILL.md                 the whole system in one file (Option 2)
templates/clip-log-template.md              event catalogue format
templates/script-template.md                voiceover script format
clips/                                      put raw recordings here (git-ignored)
work/                                       analysis files (git-ignored)
shorts/NN-slug/                             one folder per Short (git-ignored)
    rough_cut.mp4
    script.md
    voice/
    final.mp4
```

Video, audio and the contents of `clips/`, `work/` and `shorts/` are git-ignored, so your footage
and output never get committed.

## A note on rights

Most publishers tolerate fan gameplay footage for non-commercial use, but that is not blanket
permission. Avoid pre-release or leaked footage, story endings, cutscene compilations, big plot
reveals, isolated in-game music, cheats and mods. Buying a game does not grant commercial rights to
its footage — check the publisher's own policy before monetising anything.

The system is built to be honest about what the footage shows. It will not invent a reaction,
overstate a result or write a claim it cannot verify on screen.

## Licence

MIT — see [LICENSE](LICENSE).

## Built by

Built by Nickshana — NickShana Studio, a creative studio for ambitious brands.

Website: https://nickshana.com

Instagram / X / Threads: @nickshanastudio
