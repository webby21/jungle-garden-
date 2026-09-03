# Massbar — The Jungle Garden

A single-file, scroll-driven story site for the creative agency **Massbar**.

> Deep in the jungle, all the animals decided to build the most beautiful
> garden. The elephants brought the water, the monkeys planted the seeds, the
> deer collected the flowers, the parrots spread the word.
>
> Everyone was working hard. But nothing was growing.
>
> Then the Owl gathered everyone, listened, and made one clear plan — with a
> role for each of them. Slowly, the garden began to bloom.
>
> *"Great things don't happen when everyone simply works hard. They happen when
> everyone understands the same idea."* — The Owl

## Running it

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

No build step, no framework, no bundler. GSAP + ScrollTrigger load from CDN;
everything else is inline.

## Artwork

The supplied artwork *is* the site — there are no drawn stand-ins. Put the
files in `assets/` and see [`assets/README.md`](assets/README.md) for the
filenames, where each scene's copy sits, and the owl eye-tracking calibration.

## The beats

| # | Image | Beat |
|---|---|---|
| — | `hero.mp4` over `hero-poster.jpg` | We build stories people remember |
| — | the cut-out owl descends | Chapter One — The Garden |
| 01 | `elephant.jpg` | Elephants — brought the water |
| 01 | `monkeys.jpg` | Monkeys — planted the seeds |
| 01 | `deer.jpg` | Deer — collected the flowers |
| 01 | `parrots.jpg` | Parrots — spread the word |
| **02** | `parrots-dim.jpg` | Everyone was working hard. But **nothing was growing** |
| **03** | `owl-scene.jpg` | Then the Owl gathered everyone and made **one clear plan** |
| **04** | `together.jpg` | Slowly, **the garden began to bloom** → Different strengths. One vision. |
| — | the cut-out owl, close | The story is only beginning |

Then: the Owl's line, *every brand has its own jungle*, Capabilities (four
roles, one plan), and the closing CTA.

The turn is the point of the whole thing — Chapter Two is the same parrots
frame with the colour drained out of it, and Chapter Three floods it back in.
Both are plain cross-fades between files, so nothing expensive runs at scroll
time.

## What's inside

- **Chapter One is one pinned stage.** Scroll position drives a single GSAP
  timeline across five full-bleed plates of the artwork. The plates
  cross-dissolve and the camera pushes across each one, so the chapter reads as
  one continuous world and scrubbing backwards un-tells it.
- **The garden accumulates in the photography itself**: watered soil → first
  sprout → sprout and blooms → the finished garden.
- **Nothing is cropped.** Each plate is contained, not cover-cropped, and the
  camera settles on the complete frame — so the action in every scene (hands in
  the soil, the water landing, the sign) is always visible. The space around a
  contained plate is filled with a blurred copy of the same frame, so the stage
  still reads edge to edge.
- **Readable type over busy photographs.** All copy lives in a 12-column
  safe-area grid, so it can never touch an edge or overflow. Each scene sits on
  the side away from its subject and carries a directional scrim, so text is
  always on a controlled dark field.
- **The owl** narrates. It descends into the chapter as a cut-out, stands on
  the rock in the payoff plate, and the chapter closes by moving the camera
  into its eyes. Its pupils follow the cursor — the artwork's eyes are knocked
  out, so the page paints the eye-whites and moves live pupils inside them.
- **One shared rAF loop** drives eye tracking, hero parallax and the ambient
  pollen particles that drift away from the cursor.
- **Hero video**: `assets/hero.mp4` plays behind the headline — silent, 12s,
  seamlessly looping. It layers over its own first frame and only fades in once
  it is actually playing, so a missing file, a blocked autoplay, reduced motion
  or a metered connection all just leave the still. See
  [`assets/README.md`](assets/README.md) for the encoding recipe.
- **Accessibility**: with `prefers-reduced-motion: reduce` (or if GSAP fails to
  load) the chapter becomes a stacked, readable photo story. No content depends
  on animation or on JavaScript.
