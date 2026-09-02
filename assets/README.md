# Assets — Massbar · The Jungle Garden

Drop the supplied artwork into this folder using the filenames below.
`index.html` references them directly, so no code changes are needed.

| File | Used for | Notes |
|---|---|---|
| `logo.png` | Header wordmark | Transparent PNG/SVG, ~30px tall at 1x |
| `hero.jpg` | Hero background | Wide, cinematic; a gradient stands in until it exists |
| `owl.png` | The narrator (hero, chapter intro, garden reveal, final transition) | Transparent PNG. **Calibrate the eye variables** — see below |
| `elephant.png` | Elephant scene | Transparent PNG |
| `monkey.png` | Monkey scene | Transparent PNG |
| `deer.png` | Deer scene | Transparent PNG |
| `parrot.png` | Parrot scene (reused 5×, different depths/speeds) | Transparent PNG, facing right |

Until a file exists, a stylised SVG stand-in is shown in its place, so the
composition and choreography stay intact while artwork is being produced.

## Calibrating the owl's eyes

The pupils are separate DOM elements layered over the artwork. After adding
`owl.png`, adjust these variables at the top of `index.html`:

```css
--owl-left-eye-x: 41.5%;   /* centre of the left eye, % of the image box  */
--owl-left-eye-y: 33%;
--owl-right-eye-x: 58.5%;
--owl-right-eye-y: 33%;
--owl-eye-size: clamp(14px, 2.1vw, 26px);  /* socket size */
--owl-pupil-travel: 26%;                    /* max pupil offset */
```

## Tuning the composition

Each animal is placed with its own variables, so scenes can be re-staged
without touching the animation code:

```css
--elephant-x / --elephant-y / --elephant-w
--monkey-x   / --monkey-y   / --monkey-w
--deer-x     / --deer-y     / --deer-w
--parrot-x   / --parrot-y   / --parrot-w
--owl-x      / --owl-y      / --owl-w
```

Mobile overrides for the same variables live in the `max-width: 860px`
media query.
