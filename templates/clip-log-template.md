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
