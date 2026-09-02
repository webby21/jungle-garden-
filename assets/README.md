# Assets — Massbar · The Jungle Garden

Drop the supplied artwork into this folder using the filenames below.
`index.html` references them directly — no code changes needed.

| File | Used for | Notes |
|---|---|---|
| `owl.png` | The narrator — hero, chapter intro, garden reveal, final transition | **Transparent PNG.** Calibrate the eyes (below) |
| `elephant.jpg` | Scene 01 — elephants bring the water | Full scene, landscape |
| `monkeys.jpg` | Scene 02 — monkeys plant the seeds | Full scene, landscape |
| `deer.jpg` | Scene 03 — deer collect the flowers | Full scene, landscape |
| `parrots.jpg` | Scene 04 — parrots, the finished garden | Full scene, landscape |
| `hero.jpg` | Opening establishing shot | Optional — falls back to `parrots.jpg` |
| `logo.png` | Header logo | Optional — a wordmark shows until it exists |

**Extensions are forgiving.** If a scene was exported as a PNG, the page
retries `.png` automatically (and vice versa), so `elephant.png` works
without editing anything.

Every scene image is used **full-bleed**: it fills the viewport and the camera
pushes across it. Landscape, roughly 3:2 or 4:3, 1600px wide or more is ideal.
Keep the subject away from the very edges — the frame is cropped to whatever
shape the visitor's screen is.

## Where the words sit

Each scene declares which side its copy sits on, chosen to stay clear of that
image's subject, and gets a matching dark gradient behind the text:

| Scene | Subject | Copy sits |
|---|---|---|
| Elephants | left of frame | right |
| Monkeys | centre | left |
| Deer | right of frame | left |
| Parrots | left and right | bottom centre |

If you swap an image for one composed differently, change that plate's
`data-align` and its `plate__scrim--*` class in `index.html` to match. On
phones every scene switches to a bottom-anchored layout automatically.

The `--focal` value on each plate's `<img>` sets the crop's focal point
(`object-position`) — nudge it if a subject drifts out of frame on narrow
screens.

## Calibrating the owl's eyes

The pupils are live DOM elements drawn on top of the artwork, and a disc in
`--owl-eye-fill` covers the pupils painted into the PNG so they don't double
up. **Add `?calibrate` to the URL** to outline the sockets, then adjust these
values at the top of `index.html` until they sit dead centre on the eyes:

```css
--owl-left-eye-x: 40.5%;   /* centre of the left eye, % of the image box */
--owl-left-eye-y: 39.5%;
--owl-right-eye-x: 60%;
--owl-right-eye-y: 39%;

--owl-eye-size: 13.5%;     /* socket diameter, % of image width — match the eye-white */
--owl-eye-fill: #ffffff;   /* colour of the artwork's eye-white */
--owl-pupil-size: .46;     /* pupil / socket ratio */
--owl-pupil-travel: 23%;   /* how far a pupil may travel */
```

Eye tracking is disabled on touch devices and when the visitor prefers
reduced motion.
