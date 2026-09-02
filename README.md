# Massbar — The Jungle Garden

A single-file, scroll-driven story site for the fictional creative agency
**Massbar**.

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

Place the supplied artwork in `assets/` — see [`assets/README.md`](assets/README.md)
for filenames, the owl eye-tracking calibration, and the composition variables.
Stylised SVG stand-ins are shown for any file that is missing.

## What's inside

- **Chapter One** is one pinned, continuous jungle world. Scroll position drives
  a single GSAP timeline: elephant → water → monkey → seeds → deer → flowers →
  parrots → garden reveal. Nothing is reset between scenes, so the garden
  visibly accumulates and scrubbing backwards un-tells the story.
- **The owl** narrates. Its pupils follow the cursor in every scene, and the
  chapter closes by moving the camera into its eyes.
- **Pointer field**: one shared rAF loop drives eye tracking, layered mouse
  parallax and the ambient pollen particles that drift away from the cursor.
- **Accessibility**: with `prefers-reduced-motion: reduce` (or if GSAP fails to
  load) the site switches to a static mode — the garden is shown already grown
  and the story is presented as plain, readable text. No content depends on
  animation or on JavaScript.
