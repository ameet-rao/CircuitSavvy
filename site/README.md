# CircuitSavvy site

A hand-built, one-page replacement for circuitsavvy.org. It's plain HTML and CSS with no framework, no build step and no JavaScript.

```
site/
  index.html     all content
  styles.css     all styling (tokens at the top)
  favicon.svg
  images/        WebP photos (36–69 KB each) + og-card.png (social share image)
```

To preview it, open `index.html` in a browser. To deploy, upload the `site/` folder to any static host (Netlify, Cloudflare Pages, GitHub Pages).

## Design

- **Idea:** a Swiss-grid engineering document. Graph-paper background, numbered sections (01–05), figure captions ("Fig. 2.3"), a title block, and a flight-profile line drawing in the hero.
- **Type:** Helvetica Neue for everything. It's installed on Macs and iPhones. Windows falls back to Arial, and Linux to Nimbus Sans if present. Helvetica Neue can't be self-hosted for free. To make every visitor see it, license a webfont (e.g. Neue Haas Unica or Helvetica Now from Monotype) and add it to `--font`.
- **Color:** paper `#EEECE6`, ink `#121211`, and one accent, international orange `#FF4F00`. Small orange text uses `#B83700` and large orange headings use `#E84800`, so both meet WCAG contrast on paper.
- **Motion:** one choreographed page load, all in CSS. The header rule draws in, the headline slides up, then the flight path draws with the payload riding it to apogee. Hover states are small. All motion is off for visitors who turn on reduced motion. Content never depends on JS to be visible.

## Changes from the current site

- Removed the empty label and tagline slots. The Process section is now in the nav.
- No carousel and no duplicate photos. Each photo is used once, with accurate alt text.
- Dropped the CAD diagram of unknown origin and the screenshot showing students' full names. Name tags in the laptop photo are blurred.
- Photos went from 450–840 KB PNGs to 36–69 KB WebP files (about 5.3 MB down to about 310 KB).
- Fixed the bio typo, and the headline is now a clean `<h1>`. The contact section has three pre-filled email links (school, support, get involved).
- Added a new **Ideas** section. It lists seven research questions transcribed from the brainstorming whiteboard photo, with first names removed. Check the wording with the students before publishing.
- There are no analytics scripts. Add Google Analytics back only if you want it.
