# Massbar — The Jungle Garden

A single-file, scroll-driven story site for the creative agency **Massbar**.

> Deep in the jungle, all the animals decided to build the most beautiful
> garden. The elephants brought the water, the monkeys planted the seeds, the
> deer collected the flowers, the parrots spread the word — and the owl saw how
> all of it fit together.
>
> **Different strengths. One vision.**

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

## The five plates

| Beat | Image | Copy |
|---|---|---|
| Hero | `hero.mp4` over `hero-poster.jpg` | We build stories people remember |
| Chapter intro | the cut-out owl descends | Chapter One — The Garden |
| 01 | `elephant.jpg` | Elephants — brought the water |
| 02 | `monkeys.jpg` | Monkeys — planted the seeds |
| 03 | `deer.jpg` | Deer — collected the flowers |
| 04 | `parrots.jpg` | Parrots — spread the word |
| 05 | `together.jpg` | Different strengths. One vision. |
| Transition | the cut-out owl, close | The story is only beginning |

## What's inside

- **Chapter One is one pinned stage.** Scroll position drives a single GSAP
  timeline across five full-bleed plates of the artwork. The plates
  cross-dissolve and the camera pushes across each one, so the chapter reads as
  one continuous world and scrubbing backwards un-tells it.
- **The garden accumulates in the photography itself**: watered soil → first
  sprout → sprout and blooms → the finished garden.
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
