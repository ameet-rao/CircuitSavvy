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
  - an animated gradient hero with a slanted bottom edge and floating photo cards
  - a dark stats section with gradient numbers
  - white process cards that lift on hover
  - a bordered team card
  - the gradient returning as a slanted band behind the contact section
- **Colors** are CircuitSavvy's own: blue `#0073F3`, cyan `#19C3FF` and orange `#FF6A1F` on white and navy `#0B1B34`.
- **Type:** Helvetica Neue throughout. Windows falls back to Arial.
- **Motion:** the hero loads in a staggered sequence (headline, subtitle, button, then the cards). The gradient drifts slowly, and the cards bob gently. Sections fade up as you scroll in browsers that support CSS scroll-driven animation; everywhere else they're simply visible. Animation is off for visitors who turn on reduced motion.
- **Content** is the same as the original site, with the "oppurtunities" typo fixed.
