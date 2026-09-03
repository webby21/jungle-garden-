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
| `*-bg.jpg` | 64px blurred backdrop for each scene (generated, <1 KB each) |
| `hero.mp4` | Hero background video — silent, 12s, seamless loop |
| `hero.webm` | Smaller VP9 version of it, tried first |
| `hero-poster.jpg` | The video's first frame — the still shown until it plays |

Every scene image is shown **whole** — `object-fit: contain`, never cropped —
so you can always see what the animal is actually doing. The camera pushes
gently from 1.05 to 1.00, settling on the complete frame.

The space left around a contained image is filled with a heavily blurred copy
of the same frame, so the stage still reads edge to edge rather than
letterboxed. Those backdrops are the `*-bg.jpg` files: 64px wide, under 1 KB
each. Upscaling them *is* the blur, so the browser never runs an expensive
filter over a full-size photograph.

**If you add or replace a scene image**, regenerate its backdrop:

```python
from PIL import Image, ImageFilter
im = Image.open("assets/deer.jpg").convert("RGB")
sm = im.resize((64, round(64 * im.height / im.width)), Image.LANCZOS)
sm.filter(ImageFilter.GaussianBlur(1.1)).save("assets/deer-bg.jpg", quality=72, optimize=True)
```

Landscape, 1400px wide or more. Because nothing is cropped, composition is
entirely yours — but keep the subject off the extreme edges so the scrim has
somewhere to sit.

If a `.jpg` is missing the page retries `.png` automatically, and vice versa.

## Optimisation

The uploaded PNGs were 16.4 MB in total — too heavy for a page a visitor
scrolls through. Scenes are now JPEG (quality 86) at their native pixel size,
the narrator keeps its alpha as a 1200px PNG, and the logo is cropped to the
mark, for **2.8 MB total**. The originals remain in git history if you ever
need them back.

If you replace an image, run it through the same treatment — a 2 MB plate is
noticeable on a phone.

## The hero video

`hero.mp4` plays behind the hero headline. It is layered over
`hero-poster.jpg` — its own first frame, so the fade from still to video is
invisible — and only fades in once it is genuinely playing. The poster stays
put if the file is missing, the codec is unsupported, autoplay is refused, the
visitor prefers reduced motion, or they are on Save-Data / 2G. It is muted,
looping, inline, and paused whenever the hero is off screen.

**What was done to the supplied clip**

The original was 6.06s / 3.7 MB, carried a stereo AAC track, ended on a
different frame than it started, and had its `moov` atom at the end. As
shipped it is:

- **silent** — the audio track is stripped. It could never be heard behind a
  muted element, and it cost ~100 KB and risked autoplay refusals.
- **seamlessly looping** — played forward then reversed, so there is no jump
  at the loop point. 6s became a 12s round trip.
- **`+faststart`** — the `moov` atom is at the front, so playback begins
  during download instead of after it. Without this a visitor waits for the
  whole file before seeing a single frame.
- **2.4 MB** (plus a 2.1 MB VP9 `hero.webm`, tried first), re-encoded at CRF
  26 — no visible loss behind a scrim at this size.

**If you replace it**

| | |
|---|---|
| Format | H.264 MP4 (`yuv420p`, `+faststart`). Add a VP9 `hero.webm` too if you can — it is tried first and is usually 30–50% smaller |
| Audio | **None.** Strip the track entirely — it can never be heard, and a silent track still costs bytes and can block autoplay |
| Length | 6–12 seconds, cut so the last frame flows into the first |
| Size | 1280×720 is plenty (it sits behind a scrim and large type); 1920×1080 max |
| Weight | Aim under 4 MB. Over ~8 MB and phones will show the still for several seconds first |

**Encoding**

```bash
# MP4 — silent, faststart, and looped forward-then-reversed so it
# never jumps at the loop point
ffmpeg -i source.mov -filter_complex \
  "[0:v]split[a][b];[b]reverse,trim=start_frame=1,setpts=PTS-STARTPTS[r];[a][r]concat=n=2:v=1[v]" \
  -map "[v]" -an -c:v libx264 -profile:v high -pix_fmt yuv420p \
  -crf 26 -preset slow -movflags +faststart assets/hero.mp4

# WebM — smaller, tried first
ffmpeg -i assets/hero.mp4 -an -c:v libvpx-vp9 -b:v 0 -crf 36 -row-mt 1 assets/hero.webm

# the poster MUST be the video's first frame, or the fade-in jumps
ffmpeg -i assets/hero.mp4 -frames:v 1 -q:v 3 assets/hero-poster.jpg
```

If your source already loops cleanly, drop the `-filter_complex` and `-map`
lines and just use `-an ... -movflags +faststart`.

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
