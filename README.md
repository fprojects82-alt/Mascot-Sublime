# Sublime+ Landing Page

Marketing landing page for Sublime+ ("Content & social marketing, done with a
little extra"), built with Next.js (App Router), Tailwind CSS and Framer Motion,
following the Sublime+ brand identity guidelines (teal/pine/lime palette,
Poppins type, plus-mark motif).

## Getting started

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## Structure

Single page, composed in `src/app/page.tsx` from one component per section, in
order: Hero, Services, UGC, How it Works, Plans, FAQ, Final CTA.

- `src/app/page.tsx` — the landing page
- `src/app/layout.tsx`, `globals.css` — shell, brand color tokens, type
- `src/app/opengraph-image.tsx`, `icon.svg`, `sitemap.ts`, `robots.ts` — generated metadata assets
- `src/components/sections/` — one component per section
- `src/components/booking/` — Cal.com popup embed (`CalProvider` initialises it, `BookMeetingButton` opens it)
- `src/components/ui/` — `FeatureCarousel`, `CinematicFooter`
- `src/components/theme/` — light/dark theme context and toggle
- `src/components/` — shared primitives: `Nav`, `PlusMark`, `PlusField`, `Reveal`, `AnimatedSection`, `SpotlightCard`, `TopoBackground`, `ScrollProgress`, `CursorReactive`, `JsonLd`
- `src/lib/` — `site.ts` (site identity), `cal.ts` (booking config), `faq.ts` (FAQ content)
- `public/showcase/` — self-hosted UGC sample imagery
- `public/llms.txt` — plain-language brand facts for language models
- `docs/sop-copy-map.md` — SOP → copy traceability map
- `design/` — original mascot artwork; not served by the site

## Configuration

Both variables have fallbacks, so the site builds and runs without them. Set
both in the production environment.

```bash
NEXT_PUBLIC_SITE_URL=https://sublimeplus.co
NEXT_PUBLIC_CAL_LINK=username/event-slug
```

- `NEXT_PUBLIC_SITE_URL` drives canonical URLs, Open Graph image resolution,
  `sitemap.xml` and `robots.txt`. It falls back to the Vercel production URL, so
  until it is set the canonicals point at where the site actually is rather than
  at a domain that may not be owned yet.
- `NEXT_PUBLIC_CAL_LINK` is the Cal.com event path that every call-to-action
  opens. The fallback only resolves once a Cal.com account and event exist at
  that path, so bookings do not work until this is pointed at a real event.

## Content standards

Every claim on the site must trace to a Sublime+ SOP or a signed-off business
fact. `docs/sop-copy-map.md` is that map, clause by clause, and its rule is: if
a statement is not traceable to a row in it, it does not ship. Do not add
testimonials, statistics, client names or capability claims without a written
source, and update the map in the same change as the copy.

## Known gaps

- Logo is a code-recreated wordmark + plus mark (Poppins + SVG) rather than the
  original hand-lettered files. Swap in the real logo under `public/` and update
  `src/components/PlusMark.tsx` when available.
- `NEXT_PUBLIC_CAL_LINK` still points at a placeholder event path by default.
  Bookings are live only once it targets a real Cal.com event.
- Some scaffolding from removed features is still present: `src/lib/calendar.ts`
  (unused since Cal.com replaced the hand-built booking modal), the
  `gray-matter`, `next-mdx-remote` and `reading-time` dependencies (unused since
  the blog was removed), and the `images.remotePatterns` entry for Unsplash in
  `next.config.ts` (no Unsplash image is referenced any more).
