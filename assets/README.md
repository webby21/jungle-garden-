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
