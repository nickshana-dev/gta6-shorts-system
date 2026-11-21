# gta6-shorts-system

Turns raw gameplay recordings into ready-to-post vertical Shorts.

It is a set of instructions for [Claude Code](https://claude.com/claude-code) — a `CLAUDE.md` with
the rules and a skill with the production playbook. Claude reads your footage, finds the moments
worth posting, cuts them to 9:16, writes the voiceover script, and assembles the final edit with
captions and a proper audio mix. You approve what gets made and you supply the voice.

Written for a GTA VI channel, but nothing in it is game-specific — it works for any gameplay
capture, on console or PC.

## What it does

- **Probes** every clip: resolution, fps, codec, HDR, and whether the recording copied correctly.
- **Analyses densely** — audio transient detection, scene-change scores, HUD/state cues and speech
  transcription, then verifies every flagged moment on screen. Action happens in 1–3 second bursts,
  so sampling alone misses it.
- **Catalogues** everything into an event log: crashes, fights, NPC behaviour, physics, scenery,
  in-game tooltips that reveal mechanics.
- **Ranks** candidate Shorts with a viral score, and waits for you to approve before cutting.
- **Cuts** 9:16 from the originals, keeping the subject framed and HUD and burned-in subtitles out.
- **Writes** a timed voiceover script from what the footage actually shows.
- **Assembles** the final: voice synced to picture, game audio ducked (never muted), word-timed
  captions in fixed positions, mastered to −14 LUFS.

## What you need

- **A Claude Pro plan or higher** — this includes Claude Code.
- **The Claude desktop app, or the Claude Code CLI.**
- **ffmpeg** (a full build, with `libass` and `zimg`).
- **Python 3** with `numpy`, `pillow` and `faster-whisper`.
- **A voiceover source** — optional. ElevenLabs works well; so does your own microphone.
- **Recorded gameplay.** Any capture that produces a video file.

## Quick setup

**1. Get the repo**

```
git clone https://github.com/nickshana-dev/gta6-shorts-system.git
cd gta6-shorts-system
```

**2. Install ffmpeg**

```
# Windows
winget install --id Gyan.FFmpeg --accept-source-agreements --accept-package-agreements

# macOS
brew install ffmpeg
```

Restart your shell, then check `ffmpeg -version` shows `--enable-libass` and `--enable-libzimg`.

**3. Install the Python packages**

```
pip install numpy pillow faster-whisper
python -c "from faster_whisper import WhisperModel; WhisperModel('base.en', device='cpu', compute_type='int8')"
```

**4. Fill in your details**

Open `CLAUDE.md` and replace the placeholders in the table near the top — channel name, game,
capture source, brand colours, caption font and style, voice style. Install your caption font if
you don't have it.

**5. Add footage and start**

Drop your recordings into `clips/`, open the folder in Claude Code and ask it to analyse the
footage. It reads `CLAUDE.md` and the skill automatically.

## How to use it

> **TODO — write this up properly.**

### First run
TODO: what to say to Claude, what the first analysis pass produces, roughly how long it takes.

### Approving Shorts
TODO: reading the ranked candidate table, what the viral scores mean, how to pick.

### Adding the voice
TODO: generating the voiceover, settings, naming and where files go.

### The final edit
TODO: what the final pass does, what to check before posting.

### Tips
TODO: what works, what to avoid, things learned the hard way.

## Folder structure

```
CLAUDE.md                                   the rules — fill in the placeholders first
.claude/skills/gameplay-to-shorts/SKILL.md  the production playbook (the HOW)
templates/clip-log-template.md              event catalogue format
templates/script-template.md                voiceover script format
clips/                                      drop raw recordings here (git-ignored)
work/                                       proxies, contact sheets, clip log (git-ignored)
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

The system is also built to be honest about what the footage shows. It will not invent a reaction,
overstate a result or write a claim it cannot verify on screen.

## Licence

MIT — see [LICENSE](LICENSE).

## Built by

Built by Nickshana — NickShana Studio, a creative studio for ambitious brands.

Website: https://nickshana.com

Instagram / X / Threads: @nickshanastudio
