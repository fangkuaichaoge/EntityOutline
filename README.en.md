# EntityOutline

Draws a **cartoon outline around entities and models** in Minecraft Bedrock
(Android, arm64), with an optional glow.

---

## Options

| Option | What it does | Default | Range |
|---|---|---|---|
| **Outline Models** | turns the outline on/off for all models | on | – |
| **Outline Width (at 1 block)** | how thick the outline is | `0.20` | 0.05 – 16.0 |
| **Face Grow (in-plane)** | closes gaps at corners; keep it above 0 | `1.0` | 0 – 4 |
| **Normal Push (per-face)** | extra thickness along the surface normal | `0.0` | 0 – 1 |
| **Glow (additive halo)** | adds a soft glow around the outline | off | – |
| **Glow Spread** | how far the glow reaches | `2.0` | 0.5 – 6 |
| **Glow Layers** | glow smoothness (more layers = more cost) | `3` | 1 – 5 |
| **Glow Brightness** | glow strength | `2.0` | 0.2 – 8 |
| **Outline Color** | `#RRGGBB` or `#AARRGGBB` | `#000000` | – |
| **Outline Alpha** | outline opacity (must be > 0 to see anything) | `1.0` | 0 – 1 |

Settings are saved to `<mod dir>/config/entityoutline.json` and reload on the
next start.

---

## How to pick the width

The outline gets thicker the further a part is from the model's centre, so the
number is a **ratio, not a pixel count**:

* `0.20` = very thin (the default is meant to be raised);
* `2` – `6` = a clearly visible cartoon outline;
* want it thicker still? Add `Normal Push` (0.2 – 0.5) instead of a huge width,
  and keep `Face Grow` at 1 or higher.

---

## Recommended settings

Plain black outline:

```
Outline Models              on
Outline Width (at 1 block)  4.0
Face Grow (in-plane)        1.0
Normal Push (per-face)      0.0
Glow                        off
Outline Color               #000000
Outline Alpha               1.0
```

Glowing outline:

```
Outline Models              on
Outline Width (at 1 block)  4.0
Face Grow (in-plane)        1.0
Normal Push (per-face)      0.0
Glow                        on
Glow Layers                 3
Glow Brightness             2.0
Glow Spread                 2.0
Outline Color               #FFD24A      <- must be a BRIGHT colour
Outline Alpha               1.0
```

> The glow **adds** light to the screen, so a black colour cannot glow.
> Extreme values are capped automatically, so the screen cannot be washed out.

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| No outline at all | Make sure the mod is enabled and the master switch is on. |
| Outline breaks open at corners | Set `Face Grow` above 0 and `Normal Push` back to 0. |
| One model has no outline | Raise `Normal Push` to ~0.2 (its parts may sit on the centre). |
| Screen too bright / washed out | Lower `Glow Brightness`, then `Glow Layers`. |
| Nothing visible even when enabled | Check `Outline Alpha` is not 0. |
| Blocks are not outlined | Normal behaviour — this mod only outlines entities/models. |
| Performance | Each outlined draw runs twice; with Glow, `layers + 1` times. Lower the width or turn Glow off. |
