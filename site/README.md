# CircuitSavvy site

A hand-built, one-page site for circuitsavvy.org. It's plain HTML and CSS with no framework, no build step and no JavaScript.

```
site/
  index.html     all content
  styles.css     all styling (color tokens at the top)
  favicon.svg
  images/        WebP photos + og-card.png (social share image)
```

Live at https://ameet-rao.github.io/CircuitSavvy/. Every push that changes `site/` redeploys automatically (see `.github/workflows/pages.yml`).

## Design

- **Layout** borrows ideas from Stripe's homepage, with no navbar:
  - a hero with a slanted bottom edge over a dimmed rocket-launch photo (`images/hero-launch.webp`), with floating photo cards
  - a dark navy stats section
  - white process cards that lift on hover
  - a light-blue-bordered team card
  - a slanted light-blue band behind the contact section
- **Colors:** no gradients. It uses navy `#0B1B34`, white and light blue (`#8FD0FF` on dark backgrounds, `#1E90E8` where it has to read on white, `#D6ECFF` for fills).
- **Type:** Helvetica Neue throughout. Windows falls back to Arial.
- **Motion:** the hero loads in a staggered sequence (headline, subtitle, button, then the cards), and the cards bob gently. Sections fade up as you scroll in browsers that support CSS scroll-driven animation; everywhere else they're simply visible. Animation is off for visitors who turn on reduced motion.
- **Content** is the same as the original site, with the "oppurtunities" typo fixed.
