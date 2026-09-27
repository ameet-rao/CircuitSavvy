# CircuitSavvy.org — Site Reference Summary

Captured **2026-09-27** from https://circuitsavvy.org/ as a design and content reference.

---

## 0. What's in this folder

```
site-summary.md          ← this file
pages/
  index.html             ← raw server-rendered HTML of https://circuitsavvy.org/
  _404-error-page.html   ← what the server returns for any unknown path
meta/
  sitemap.xml, robots.txt, llms.txt
assets/
  images/   11 unique images (renamed descriptively; see §9)
  css/      site-styles-tailwind.css (compiled Tailwind v4 + theme tokens)
            google-fonts-inter-700.css        (original Google Fonts CSS, remote URLs)
            google-fonts-inter-700.local.css  (same, rewritten to point at ../fonts/)
  js/       app-runtime-react-router.js   (React + TanStack Router runtime bundle)
            app-homepage-route.js          (the homepage component: all content + image refs)
            third-party/google-analytics-gtag.js, third-party/lovable-flock-analytics.js
  fonts/    Inter Bold (700) .woff2, 7 unicode-range subsets
```

The raw HTML in `pages/` still references the site's original absolute paths (`/assets/...`, `/__l5e/...`). It's there to read, not to open offline. Use the renamed files in `assets/` together with the mapping in §9.

**Tech stack (inferred):** built with **Lovable** (the `/__l5e/assets-v1/` image paths, the `~flock.js` analytics and the `r2.dev` "lovp_" OG image). It runs **React + TanStack Start/Router** with server-side rendering and hydration, **Tailwind CSS v4** and **shadcn/ui**-style tokens and components (the carousel is shadcn's Embla carousel). Icons are **lucide** (inline SVG).

---

## 1. Site map

The sitemap lists **one URL**, and the JS router defines **one route (`/`)**. It's a **single-page, one-scroll site** that uses in-page anchors for navigation.

| URL | Status | Purpose |
|---|---|---|
| `https://circuitsavvy.org/` | 200 | Home. The whole site: hero, impact stats, 4-step process, team, contact. |
| `#top` | anchor | Hero (logo link target) |
| `#impact` | anchor | Impact stats (nav: "Impact") |
| `#process` | anchor | "The Process" 4-step section (**not linked from the nav**) |
| `#team` | anchor | Team / founder bio (nav: "Team") |
| `#contact` | anchor | Contact (nav: "Contact") |
| any other path | 404 | Generic "404 Page not found" page with a "Go home" link |

Probed paths that return 404: `/about`, `/team`, `/contact`, `/index.html`, `/favicon.ico`, `/apple-touch-icon.png`, `/manifest.json`, `/site.webmanifest`.

`robots.txt` allows all crawlers (Googlebot, Bingbot, Twitterbot, facebookexternalhit, `*`) and points to the sitemap.

`llms.txt` (a plain-text summary for AI tools) also lists just the one Home page. It summarizes the program (the 4-step process and the impact numbers), the founder, and contact details (hello@circuitsavvy.org, ameetrao.com, LinkedIn). It says nothing that isn't already on the homepage.

---

## 2. Meta info

### Home (`/`)
| Tag | Value |
|---|---|
| `<title>` | CircuitSavvy — Delaware Aerospace Engineering for Students |
| meta description | CircuitSavvy gives Delaware students hands-on aerospace engineering: 45 students, 700+ learning hours, and 4 NASA TechRise payload proposals. |
| og:title / twitter:title | CircuitSavvy — Delaware Aerospace Engineering for Students |
| og:description / twitter:description | Hands-on aerospace engineering for Delaware students: 45 students, 700+ learning hours, 4 NASA TechRise proposals. |
| og:type | website |
| og:url / canonical | https://circuitsavvy.org/ |
| og:site_name | CircuitSavvy |
| og:image / twitter:image | 1920×1080 screenshot of the hero (→ `assets/images/social-share-og-image-homepage-screenshot.png`) |
| twitter:card | summary_large_image |
| author | Ameet Rao |
| robots | index, follow, max-image-preview:large |
| google-site-verification | present |
| favicon | `/favicon.png` (64×64, "CS" monogram with a rocket) |
| lang | `en` |
| Analytics | Google Analytics 4 (`G-14JZTQKNM4`) + Lovable "flock" analytics (proxied via `/~api/analytics`, sends to Tinybird) |

**Structured data (JSON-LD), two blocks:**
- `Organization`: name CircuitSavvy, email hello@circuitsavvy.org, areaServed "Delaware, USA", founder Ameet Rao (ameetrao.com), sameAs LinkedIn.
- `EducationalOrganization`: slogan *"Creating the future of Aerospace Engineers in Delaware"*, a description that mentions NASA TechRise, 45 students and 700+ hours, areaServed State: Delaware.

### 404 page
| Tag | Value |
|---|---|
| `<title>` | CircuitSavvy — Aerospace STEM for Delaware Students *(differs from the homepage title)* |
| Body | H1-style "404", "Page not found", "The page you're looking for doesn't exist or has been moved.", link **Go home** |

---

## 3. Navigation

### Main header (fixed, translucent, blurred)
- **Logo / wordmark:** "Circuit**Savvy**" ("Savvy" in primary blue), links to `#top`
- **Primary nav** (`aria-label="Primary navigation"`), right-aligned, small bold text:
  - Impact → `#impact`
  - Team → `#team`
  - Contact → `#contact`
- No hamburger menu. The three links stay inline on mobile (`gap-4` → `sm:gap-8`).
- No header CTA button.

### Footer
- Left: "© 2026 CircuitSavvy. All rights reserved."
- Right: "Created by Ameet Rao"
- **No links** in the footer (no nav repeat, socials, email or privacy page).

### Outbound links (whole site)
| Link | Where | Status |
|---|---|---|
| `https://www.linkedin.com/in/ameetrao` | Team card icon button | LinkedIn returns 999 to bots (normal; not verifiable by script) |
| `https://ameetrao.com` | Team card icon button | 200 OK |
| `mailto:hello@circuitsavvy.org` | Contact section | n/a |

---

## 4. Page content: Home, section by section

Section order and background treatment alternate: **canvas (light blue) → surface-strong (near-white, bordered) → background → surface-strong → background → footer surface-strong**.

### 4.1 Hero (`#top`)
- **H1:** "Circuit**Savvy**" (the two halves in two colors), with a subtitle span *inside the H1*: "Bringing Aerospace Engineering to Students"
- **Eyebrow label** above the H1: the element exists (orange, uppercase, letter-spaced) but is **empty**
- **Italic tagline** under the H1: the element exists but is **empty**
- **Right column:** image carousel of 6 slides, each with a "01 / 06" style counter, plus round Previous/Next arrow buttons below
- **CTAs:** none (no button in the hero)

Carousel slides (alt text as written on the site):
1. Students watching a research proposal presentation in class
2. Students collaborating on laptops during a CircuitSavvy session
3. Students reviewing a NASA research proposal presentation in class *(same image file as slide 1)*
4. A full classroom of students during a CircuitSavvy workshop
5. Whiteboard of student space experiment ideas *(same image file as Process step 2)*
6. Students discussing payload ideas around lab tables

### 4.2 Impact (`#impact`)
- **H2:** "Our impact **measured** in real work." ("measured" in primary blue)
- **Stat row** (3 columns with vertical dividers on desktop, stacked on mobile):
  | Number | Label | Number color |
  |---|---|---|
  | **45** | students in program | blue |
  | **700+** | hours of learning across all students | orange |
  | **4** | NASA aerospace engineering proposals made | blue |
- CTAs: none

### 4.3 The Process (`#process`)
- **Eyebrow:** empty element
- **H2:** "The Process"
- **4 rows**, each with a big numbered blue circle, an H3 with a description, and an illustrative image on the right:

| # | H3 | Body copy (summary) | Image |
|---|---|---|---|
| 1 | **Learning** | Students learn how payloads work in space, atmospheric conditions, and what to account for when designing for space. | CAD diagram of a two-stage payload isolation platform (labelled magnetic shield, titanium blades) |
| 2 | **Brainstorming** | Students take control. They come up with ideas, and the group iterates on them together, turning them into NASA research studies. | Whiteboard of students' experiment ideas |
| 3 | **Drafting** | Students draft proposals for the NASA TechRise Student Challenge, with a full design description, schematics and hardware specifics. | Screenshot of a proposal-summary table |
| 4 | **Creating** | Students can launch their experiment to space if they win a grant through the TechRise Challenge. | Student assembling a clear acrylic payload enclosure with a screwdriver |

- CTAs: none

### 4.4 The Team (`#team`)
- **Eyebrow:** empty element
- **H2:** "The Team"
- **Profile card** (single person): round headshot, H3 **Ameet Rao**, and a bio: a 17-year-old from Delaware who started CircuitSavvy to lower the barrier to entry into engineering and bring STEM opportunities to under-resourced areas.
- **Icon buttons:** LinkedIn, personal website (round, outlined)

### 4.5 Contact (`#contact`)
- **Eyebrow:** empty element
- **H2:** "Reach out." (with a trailing space in the source)
- **Body:** "Want to bring CircuitSavvy to your school, support the program, or get involved? Write to hello@circuitsavvy.org."
- **CTA:** the email address is the only call to action on the whole site (`mailto:` link, blue, underlined, turns orange on hover)

### 4.6 Footer
See §3.

### Heading outline
```
H1  CircuitSavvy — Bringing Aerospace Engineering to Students
 H2  Our impact measured in real work.
 H2  The Process
  H3  Learning
  H3  Brainstorming
  H3  Drafting
  H3  Creating
 H2  The Team
  H3  Ameet Rao
 H2  Reach out.
```

### Calls to action, all of them
| CTA | Type | Target |
|---|---|---|
| hello@circuitsavvy.org | inline text link | `mailto:` |
| LinkedIn icon | icon button | linkedin.com/in/ameetrao (new tab) |
| Website icon | icon button | ameetrao.com (new tab) |
| Impact / Team / Contact | nav links | in-page anchors |

---

## 5. Forms

**None.** There are no `<form>`, `<input>`, newsletter signup or contact form. Contact is by `mailto:` only. The theme defines `--input` and `--ring` tokens (shadcn defaults), but nothing uses them.

---

## 6. Color palette

The theme colors are defined in `site-styles-tailwind.css` as `oklch()` CSS variables on `:root`. The hex/RGB values below are converted from OKLCH (sRGB, rounded).

### Colors actually used on the page
| Token | OKLCH (source) | Hex | RGB | Used for |
|---|---|---|---|---|
| `--primary` | `oklch(57% .22 253)` | **#0073F3** | rgb(0, 115, 243) | "Savvy" in the logo and H1, highlighted words, stats 1 and 3, process number circles, email link, nav hover |
| `--secondary` | `oklch(57% .14 48)` | **#B7591E** | rgb(183, 89, 30) | Eyebrow labels (empty), middle stat "700+", email link hover |
| `--accent` | `oklch(62% .14 47)` | **#C86732** | rgb(200, 103, 50) | Carousel button hover background |
| `--foreground` | `oklch(19% .035 254)` | **#081423** | rgb(8, 20, 35) | Headings, body text (near-black navy) |
| `--muted-foreground` | `oklch(45% .035 254)` | **#485769** | rgb(72, 87, 105) | Paragraph copy, nav links, captions, footer |
| `--canvas` | `oklch(91% .035 252)` | **#D1E3F9** | rgb(209, 227, 249) | Page base / hero background (light sky blue) |
| `--background` | `oklch(97.5% .008 250)` | **#F3F7FC** | rgb(243, 247, 252) | Process and Contact section backgrounds |
| `--surface` | `oklch(98.5% .006 250 / .86)` | **#F7FAFE** @ 86% | rgb(247, 250, 254) | Fixed header (with `backdrop-blur-xl`, at 90% opacity) |
| `--surface-strong` | `oklch(98.5% .006 250 / .95)` | **#F7FAFE** @ 95% | rgb(247, 250, 254) | Impact, Team, footer bands; carousel buttons |
| `--border` | `oklch(19% .035 254 / .16)` | **#081423** @ 16% | rgb(8, 20, 35) | Hairline dividers, image borders |
| `--primary-foreground` | `oklch(99% .004 250)` | **#FAFCFE** | rgb(250, 252, 254) | Numbers inside the blue process circles |

**In short:** an electric blue (#0073F3) and a burnt orange (#B7591E) on pale blue and white, with near-black navy text. It's a complementary blue and orange scheme.

### Defined but unused (shadcn theme leftovers)
| Token | Hex |
|---|---|
| `--muted` | #E2E9F0 |
| `--card` / `--popover` | #FAFCFE |
| `--destructive` | #E7000B |
| `--chart-1…5` | #0091FF, #C86732, #104E64, #FFB900, #FE9A00 |
| `--sidebar` family | #0F1923, #1D252D, #F6F9FC, #0091FF |
| `.dark` theme | Full dark palette defined (slate navy #020618-ish background), but there's no dark-mode toggle and no `prefers-color-scheme` hook |

Other hard-coded colors in the CSS: `#000`, `#fff`, `#ccc` and black at 5%, 10%, 25% and 80% alpha (shadows, overlays).

---

## 7. Typography

| Role | Font family | Weight | Sizes (mobile → sm → lg) |
|---|---|---|---|
| **All headings (h1–h6)** and `.font-heading` (logo, stats, step numbers) | **Inter** (Google Fonts, 700 only), fallback Helvetica Neue, Helvetica, Arial | 700 | see below |
| **Body / paragraphs** (`.font-sans` and the default) | **Helvetica Neue**, Helvetica, Arial, sans-serif (system font, not downloaded) | 400–600 | see below |

Only **Inter Bold (700)** is loaded, so every Inter usage on the site is bold.

### Scale in use (Tailwind classes → rem/px)
| Element | Classes | Size |
|---|---|---|
| H1 "CircuitSavvy" | `text-5xl sm:text-7xl lg:text-8xl`, `leading-[0.94]` | 48px → 72px → **96px**, tight line-height |
| H1 subtitle span | `text-xl sm:text-2xl font-medium`, 80% foreground | 20px → 24px |
| H2 Impact | `text-4xl sm:text-6xl tracking-tight leading-[1.02]` | 36px → 60px |
| H2 Process | `text-4xl sm:text-5xl leading-tight` | 36px → 48px |
| H2 Team, Contact | `text-4xl` | 36px |
| H3 process steps | `text-2xl sm:text-3xl` | 24px → 30px |
| H3 team name | `text-2xl` | 24px |
| Stat numbers | `text-6xl` Inter bold | 60px |
| Step number circles | `text-4xl sm:text-5xl` in an 80–96px circle | 36px → 48px |
| Eyebrow labels | `text-xs font-bold uppercase tracking-[0.2em]`, orange | 12px |
| Hero tagline (empty) | `text-lg sm:text-xl italic` | 18px → 20px |
| Body copy | `text-sm sm:text-base leading-relaxed` (process), `text-base` (bio), `text-lg` (contact) | 14–18px, line-height 1.625 |
| Stat labels | `text-sm leading-relaxed`, max-width 15rem | 14px |
| Nav links | `text-xs font-semibold` | 12px |
| Logo | `text-base font-bold` | 16px |
| Captions / footer | `text-xs` | 12px |

**Pattern:** huge, tight, bold Inter headings; small, relaxed, muted Helvetica body text. The contrast in size is very high.

---

## 8. Layout patterns and components

1. **Fixed translucent header.** Full-width, `bg-surface/90` + `backdrop-blur-xl`, hairline bottom border, container `max-w-6xl` (72rem). Sections use `scroll-mt-20` so anchors land below the header.
2. **Split hero.** Nearly full viewport (`min-h-[94svh]`), 2-column grid on large screens at `0.68fr / 1.32fr`, with the text on the left and a **wide image carousel** on the right. Slides are `basis-[88%]` / `basis-[82%]`, so the next slide peeks in from the edge. Images are 4:3, `rounded-md`, 1px border and a large blue-tinted shadow (`shadow-2xl shadow-primary/10`). The carousel uses round outline arrow buttons centered below the slides and a "01 / 06" counter under each image.
3. **Stat band.** Full-bleed white band, big H2, then a **3-column stats row** separated by vertical hairlines (horizontal ones on mobile). The numbers alternate blue, orange, blue.
4. **Numbered process list.** Not cards: each step is a 3-column row (`7rem | 0.8fr | 1.2fr`) holding the **number circle**, the **title and copy** and the **image** (max 160px tall, `object-contain`). Rows are separated by hairline borders.
5. **Section header pattern.** An orange uppercase letter-spaced **eyebrow** (currently empty everywhere) over a big bold H2. The Process and Team sections use a 2-column `0.7fr / 1.3fr` split, with the header on the left and content on the right.
6. **Single profile card.** Round avatar (112–128px) next to the name, bio and two round icon buttons, in a `8rem | 1fr` grid.
7. **Minimal contact block.** H2 plus one paragraph with an inline mailto link. No form and no button.
8. **Two-line footer.** Copyright left, credit right.
9. **Scroll-reveal animation.** Every block starts at `opacity-0 translate-y-4` and fades or slides up over 700ms (`cubic-bezier(0.22,1,0.36,1)`), with staggered `transition-delay` of 0 / 100 / 160 / 200ms. The animation is off when the visitor has reduced motion turned on (`motion-reduce`).
10. **Section rhythm.** Vertical padding of `py-20` (80px) on mobile and `sm:py-28`/`sm:py-32` (112–128px) on larger screens. Horizontal gutter is `px-5` (20px) on mobile and `sm:px-8` (32px) above. Container widths are `max-w-6xl` for content and `max-w-7xl` for the hero. Border radius is `--radius: .625rem` (10px) and the images use `rounded-md`.

Not present: testimonials, pricing, FAQ, blog, logos/partners strip, video, newsletter, hamburger menu, dark-mode toggle.

---

## 9. Asset manifest

### Images (11 unique files; the page references 13 image URLs)
| New filename | Original URL (under `https://circuitsavvy.org`) | Px | Size | Used in | Site alt text |
|---|---|---|---|---|---|
| `hero-carousel-01-students-watching-research-proposal.png` | `/__l5e/assets-v1/46c1bd85-…/image-15.png` **and** `/__l5e/assets-v1/856e472f-…/image-10.png` (identical files) | 486×649 | 456 KB | Carousel slides 1 **and 3**; also the `<link rel=preload>` | Slide 1: "Students watching a research proposal presentation in class" / Slide 3: "Students reviewing a NASA research proposal presentation in class" |
| `hero-carousel-02-students-collaborating-on-laptops.png` | `/__l5e/assets-v1/9b55f7a7-…/image-12.png` | 865×649 | 815 KB | Carousel slide 2 | Students collaborating on laptops during a CircuitSavvy session |
| `hero-carousel-04-full-classroom-workshop.png` | `/__l5e/assets-v1/b18ac398-…/image-14.png` | 865×649 | 817 KB | Carousel slide 4 | A full classroom of students during a CircuitSavvy workshop |
| `hero-carousel-06-students-discussing-around-lab-tables.png` | `/__l5e/assets-v1/ec2a838c-…/image-11.png` | 486×649 | 492 KB | Carousel slide 6 | Students discussing payload ideas around lab tables |
| `process-01-learning-payload-isolation-stage-cad-diagram.png` | `/__l5e/assets-v1/13b0ba4d-…/image-3.png` | 515×388 | 193 KB | Process step 1 | "Student-built payload enclosure with electronics on a workbench" (**doesn't match the image**, see §10) |
| `process-02-brainstorming-whiteboard-experiment-ideas.png` | `/__l5e/assets-v1/6356de46-…/image-4.png` **and** `/__l5e/assets-v1/7c6ef045-…/image-13.png` (identical files) | 865×649 | 556 KB | Process step 2 **and** carousel slide 5 | "Whiteboard covered in student experiment ideas" / "Whiteboard of student space experiment ideas" |
| `process-03-drafting-techrise-proposal-table-screenshot.png` | `/__l5e/assets-v1/737d1a2e-…/image-6.png` | 1067×763 | 443 KB | Process step 3 | Student NASA TechRise proposal summaries in a table |
| `process-04-creating-student-assembling-payload.png` | `/__l5e/assets-v1/5c449e91-…/image-2.png` | 630×418 | 447 KB | Process step 4 | Student assembling a payload with a screwdriver |
| `team-ameet-rao-headshot.png` | `/__l5e/assets-v1/22d13f9d-…/ameet.png` | 345×297 | 152 KB | Team card | Ameet Rao, founder of CircuitSavvy |
| `favicon-cs-rocket-logo-64px.png` | `/favicon.png` | 64×64 | 3.7 KB | Favicon | n/a |
| `social-share-og-image-homepage-screenshot.png` | `https://pub-bb2e103a32db4e198524a2e9ed8f35b4.r2.dev/lovp_…/a4fd93…_1790546787646.png` | 1920×1080 | 384 KB | og:image / twitter:image | n/a |

There are no CSS background images, SVG files or icon sprites. All icons (arrows, LinkedIn, globe) are inline lucide SVGs in the JS and HTML.

### CSS (3 files)
| New filename | Original | Notes |
|---|---|---|
| `site-styles-tailwind.css` | `/assets/styles-CxPC2XwA.css` (79 KB, minified) | Tailwind v4 output, theme tokens (§6), keyframes `pulse`, `enter`, `exit`, `accordion-*`, `caret-blink` |
| `google-fonts-inter-700.css` | `fonts.googleapis.com/css2?family=Inter:wght@700&display=swap` | Original, with remote font URLs |
| `google-fonts-inter-700.local.css` | *(derived)* | Same `@font-face` rules pointing at `../fonts/*.woff2` |

### JavaScript (4 files)
| New filename | Original | Notes |
|---|---|---|
| `app-runtime-react-router.js` | `/assets/index-Uxrvt3N2.js` (339 KB) | React, TanStack Router, head/meta config, JSON-LD |
| `app-homepage-route.js` | `/assets/routes-BloODoa1.js` (69 KB) | The homepage component: all copy, image paths, carousel, lucide icons |
| `third-party/lovable-flock-analytics.js` | `/~flock.js` (21 KB) | Lovable page analytics (sends to Tinybird) |
| `third-party/google-analytics-gtag.js` | `googletagmanager.com/gtag/js?id=G-14JZTQKNM4` (514 KB) | Google Analytics 4 loader |

### Fonts (7 files)
`inter-700-{latin, latin-ext, cyrillic, cyrillic-ext, greek, greek-ext, vietnamese}.woff2` from fonts.gstatic.com (Inter v20). For an English-only site you only need `latin` (24 KB) and maybe `latin-ext`. Helvetica Neue (body) is a system font and isn't downloaded by the site.

---

## 10. Findings: broken, missing or worth flagging

### Content and bugs
1. **Five empty text slots.** The hero eyebrow, hero italic tagline, and the Process, Team and Contact eyebrows are all styled `<p>` elements with no text. This leaves a big empty area under the hero H1, which is visible in the site's own OG share image: the left column is blank below the subtitle.
2. **Duplicate carousel image.** Slides 1 and 3 are the **same photo** under two URLs with different alt text.
3. **Duplicate across sections.** Carousel slide 5 and Process step 2 are the **same whiteboard photo**.
4. **Mismatched alt text.** Process step 1's image is a **CAD diagram of a two-stage isolation platform** (labelled magnetic shield and titanium blades), but its alt text says "Student-built payload enclosure with electronics on a workbench". It also looks like a third-party engineering diagram rather than student work, so check where it came from and its usage rights.
5. **Typo in the team bio:** "oppurtunities" should be "opportunities".
6. **"Reach out. "** H2 has a trailing space (harmless, but sloppy in source).
7. **The Process section isn't in the nav.** The header links only Impact, Team and Contact.
8. **Page titles don't match.** The homepage uses "…Delaware Aerospace Engineering for Students" and the 404 page uses "…Aerospace STEM for Delaware Students".

### Privacy (student names)
9. The **proposal-table screenshot** (Process step 3) shows two students' **full names** and their proposal text. The **laptop photo** (carousel slide 2) shows name tags with full names, and the **whiteboard** shows first names. Consider blurring these or confirming consent.

### Technical and performance
10. **Content is hidden without JavaScript.** Every section wrapper is server-rendered with `opacity-0 translate-y-4` and only fades in after JS hydrates. Visitors without JS, some crawlers and link-preview renderers can see a blank page.
11. **Heavy, unoptimized images.** Photos are served as PNG at 450–840 KB each (about **5.3 MB** of images for one page). WebP or AVIF, or JPEG at these sizes, would be about 5–10× smaller. There's no `srcset` or responsive sizes.
12. **The OG image is a raw hero screenshot** with the empty left column and a mostly blank lower half. It's not a designed social card.
13. **The subtitle is inside the `<h1>`**, so the H1's accessible name becomes "CircuitSavvyBringing Aerospace Engineering to Students", with no space between the two parts.
14. **No `/favicon.ico`** (it's a 404). Most browsers use the declared PNG, but some tools request `.ico` directly. There's also no apple-touch-icon and no web manifest.
15. **Only Inter 700 is loaded**, while body text uses the system Helvetica, so rendering will vary on Windows and Android, where Arial is the fallback.
16. **Unused theme tokens.** The dark theme, chart, sidebar and destructive colors are shadcn scaffolding the page never uses.
17. The footer has no links: no email, socials, privacy policy or nav repeat.

### Checked and fine
- `sitemap.xml`, `robots.txt` and `llms.txt` are valid and consistent with the single-page site. `llms.txt` spells "opportunities" correctly, so the typo is only on the live page.
- All 11 image URLs, the CSS, JS, fonts and OG image return **200**.
- The canonical URL, OG tags, Twitter card and JSON-LD are all present.
- The external link `ameetrao.com` returns 200. The LinkedIn URL can't be checked by script because it returns 999 to bots, which is normal.
- There are no broken internal links: every anchor (`#top`, `#impact`, `#team`, `#contact`) exists.
