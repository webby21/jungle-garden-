# Amsterdam Four

The story's accent lines — the chapter title, the Owl's quotation and the
closing line — are set in **Amsterdam Four**. It is a licensed font, so it is
deliberately **not** committed here.

**To switch it on:** put the web files in this folder as

```
assets/fonts/amsterdam-four.woff2
assets/fonts/amsterdam-four.woff   (optional, older browsers)
```

The `@font-face` block at the top of `index.html` already points at those exact
names, so nothing else needs changing — the font appears as soon as the files
are in place.

**Until then** the stack falls through to **Sacramento**, loaded from Google
Fonts, which is a signature script of similar weight and rhythm. Nothing looks
broken while you wait for the licence.

If your licensed files have different names, edit the two `src:` lines in the
`@font-face` rule.

## Sizing note

Signature scripts have a much smaller x-height than a normal face, so the
accent headings are set larger than their sans equivalents. If Amsterdam Four
sits noticeably bigger or smaller than Sacramento once installed, nudge
`font-size` on `.chapter-intro__title`, `.owl-quote__text`,
`.closing__title` and `.footer-brand__tag`.
