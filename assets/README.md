# Assets — Massbar · The Jungle Garden

These are the files `index.html` uses. All paths appear exactly once each in
the markup, next to a comment naming them.

| File | Used for |
|---|---|
| `owl-scene.jpg` | Hero — the owl, wings open, in its garden |
| `owl-figure.png` | The cut-out narrator (chapter intro + final transition). **Transparent PNG** |
| `elephant.jpg` | Scene 01 — elephants brought the water |
| `monkeys.jpg` | Scene 02 — monkeys planted the seeds |
| `deer.jpg` | Scene 03 — deer collected the flowers |
| `parrots.jpg` | Scene 04 — parrots spread the word |
| `together.jpg` | Scene 05 — the payoff: the whole cast in the finished garden |
| `logo.png` | Header mark, cropped to the owl |
| `hero.mp4` | **Optional** hero background video |
| `hero.webm` | **Optional** smaller version, tried before the MP4 |

Every scene image is used **full-bleed**: it fills the viewport and the camera
pushes across it. Landscape, 1400px wide or more. Keep subjects away from the
very edges — the frame is cropped to whatever shape the visitor's screen is.

If a `.jpg` is missing the page retries `.png` automatically, and vice versa.

## Optimisation

The uploaded PNGs were 16.4 MB in total — too heavy for a page a visitor
scrolls through. Scenes are now JPEG (quality 86) at their native pixel size,
the narrator keeps its alpha as a 1200px PNG, and the logo is cropped to the
mark, for **2.8 MB total**. The originals remain in git history if you ever
need them back.

If you replace an image, run it through the same treatment — a 2 MB plate is
noticeable on a phone.

## The optional hero video

Drop `hero.mp4` into this folder and it takes over the hero by itself — no
code change. It is layered over `owl-scene.jpg` and only fades in once it is
genuinely playing, so the photograph stays put if the file is missing, the
codec is unsupported, autoplay is refused, the visitor prefers reduced motion,
or they are on Save-Data / 2G. It is muted, looping, inline, and paused
whenever the hero is off screen.

**What to give it**

| | |
|---|---|
| Format | H.264 MP4 (`yuv420p`, `+faststart`). Add a VP9 `hero.webm` too if you can — it is tried first and is usually 30–50% smaller |
| Audio | **None.** Strip the track entirely — it can never be heard, and a silent track still costs bytes and can block autoplay |
| Length | 6–12 seconds, cut so the last frame flows into the first |
| Size | 1280×720 is plenty (it sits behind a scrim and large type); 1920×1080 max |
| Weight | Aim under 4 MB. Over ~8 MB and phones will show the still for several seconds first |

**Encoding**

```bash
# MP4 — the one that matters
ffmpeg -i source.mov -an -vf "scale=1280:-2" \
  -c:v libx264 -profile:v high -pix_fmt yuv420p -crf 26 -preset slow \
  -movflags +faststart assets/hero.mp4

# WebM — optional, smaller, tried first
ffmpeg -i source.mov -an -vf "scale=1280:-2" \
  -c:v libvpx-vp9 -b:v 0 -crf 34 -row-mt 1 assets/hero.webm
```

Keep it *slow* — a drifting push through the canopy, light moving on water.
The headline sits over it, so anything with fast cuts or high contrast in the
lower-left will fight the type.

GitHub warns above 50 MB per file and rejects above 100 MB, so a hero video
should never come close.

## Where the words sit

Each scene declares which side its copy sits on, chosen to stay clear of that
image's subject, and gets a matching dark gradient behind the text:

| Scene | Subject | Copy sits |
|---|---|---|
| Elephants | left of frame | right |
| Monkeys | centre | left |
| Deer | centre-right | left |
| Parrots | left and right, sign centre | bottom |
| Together | spread across the frame | bottom |

Swapping in an image composed differently means changing that plate's
`data-align` and its `plate__scrim--*` class in `index.html`. On phones every
scene switches to a bottom-anchored layout automatically, and the ensemble
plate is letterboxed rather than cropped so the whole cast survives.

The `--focal` value on each plate's `<img>` sets the crop's focal point
(`object-position`) — nudge it if a subject drifts out of frame on a narrow
screen.

## The owl's eyes

The eyes in `owl-figure.png` are knocked out of the artwork, so the page paints
its own eye-whites into those holes and moves live pupils on top. The values
below were measured from the file's alpha channel:

```css
--owl-left-eye-x: 30.05%;  --owl-left-eye-y: 42.25%;
--owl-left-eye-w: 30.9%;   --owl-left-eye-h: 26%;

--owl-right-eye-x: 62.3%;  --owl-right-eye-y: 42%;
--owl-right-eye-w: 28.2%;  --owl-right-eye-h: 26.8%;

--owl-eye-fill: #fbf7ff;   /* the eye-white painted behind the pupil */
--owl-pupil-size: .44;     /* pupil / socket ratio */
--owl-pupil-travel: 22%;   /* how far a pupil may travel */
```

**If you replace the owl artwork**, add `?calibrate` to the URL — the sockets
are outlined in gold — and adjust those values until they sit on the eyes.

Eye tracking is off on touch devices and when the visitor prefers reduced
motion.
