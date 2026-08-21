# Design sources

Original, unprocessed assets. **Nothing here is served by the site** — these are
kept for reference and for regenerating derived assets.

| File | What it is |
| --- | --- |
| `mascot-character-sheet.png` | Five-angle turnaround (front, 3/4, side, back ×2). Source for any future multi-angle mascot work. |
| `mascot-pose-pointing.png` | Raw render of the hero pose, on its original background. |

## Status: the mascot is not currently on the site

The hero is typographic (`src/components/sections/Hero.tsx` — wordmark, plus
field and an animated headline). There is no mascot image in `public/` and no
`src/components/mascot/`; the cursor-reactive behaviour that the mascot face
once used now lives in `src/components/CursorReactive.tsx` and
`src/components/usePointerVector.ts`, applied to other elements.

The artwork is retained here so the mascot can be reintroduced without
re-rendering it.

## If the mascot is reintroduced

The previous hero asset was derived from `mascot-pose-pointing.png` by:

1. Flood-filling the background to transparent from the image borders inward, so
   the mascot's own white helmet and cream sneakers are preserved.
2. Repainting the face screen as blank glass, with the eyes and mouth drawn in
   code so they can track the cursor and blink.
3. Eroding the alpha edge by ~1px to remove the halo left by anti-aliased
   background pixels.

The face overlay was positioned as percentages of the image box, so it has to be
re-measured against whatever artwork it is layered onto — it will silently
misalign otherwise.
