# BIG JADDY ENT Event Center

A modern one-page marketing website for **BIG JADDY ENT Event Center** in
Achimota, Accra. Built with [Astro](https://astro.build/), it presents the
venue, services, and occasions, and lets visitors book a tour or reach out by
phone, WhatsApp, or an inquiry form.

> Tagline: **"Where every event feels Grand."**

---

## Table of contents

- [Tech stack](#tech-stack)
- [Quick start](#quick-start)
- [Project structure](#project-structure)
- [Editing content (cheat sheet)](#editing-content-cheat-sheet)
  - [Contact details, phone, WhatsApp, email, hours](#1-contact-details)
  - [Services, occasions, gallery](#2-services-occasions-and-gallery)
  - [Images](#3-images)
  - [The logo](#4-the-logo)
  - [The inquiry form](#5-the-inquiry-form)
  - [The map](#6-the-map)
  - [Colors and fonts](#7-colors-and-fonts)
- [Design system](#design-system)
- [Before you launch (checklist)](#before-you-launch-checklist)
- [Deployment](#deployment)
- [Accessibility & performance](#accessibility--performance)
- [Credits](#credits)

---

## Tech stack

| Part | Choice |
|------|--------|
| Framework | Astro `^5.7` (static site, zero JS by default) |
| Styling | Plain CSS with custom properties (design tokens) in `src/styles/global.css`, scoped styles per component |
| Fonts | Google Fonts: **Libre Bodoni** (headings) + **Hanken Grotesk** (body) |
| Images | Unsplash CDN (remote), referenced by photo ID |
| Interactivity | A small amount of vanilla JS (scroll reveals, sticky header, mobile menu, form) |

No framework runtime (React/Vue) and no build-time CMS. Everything is editable
directly in the `.astro` files.

---

## Quick start

Requires [Node.js](https://nodejs.org/) 18.20+ (built and tested on Node 24).

```bash
npm install        # install dependencies (first time only)
npm run dev        # start the dev server at http://localhost:4321
npm run build      # build the production site into dist/
npm run preview    # preview the production build locally
```

While `npm run dev` is running, edits appear instantly in the browser. A hard
refresh (Cmd/Ctrl+Shift+R) clears any cached fonts/styles if something looks off.

---

## Project structure

```
bigjaddy/
├── public/
│   └── favicon.svg            # browser tab icon (BJ shield)
├── src/
│   ├── layouts/
│   │   └── Layout.astro       # <head>, fonts, meta tags, global scripts
│   ├── components/
│   │   ├── Header.astro       # top nav + mobile menu
│   │   ├── Hero.astro         # the big opening section
│   │   ├── Intro.astro        # "About the venue"
│   │   ├── Services.astro     # the 6 service offerings
│   │   ├── Occasions.astro    # weddings / parties / conferences / church
│   │   ├── Gallery.astro      # photo masonry
│   │   ├── Contact.astro      # details + map + inquiry form
│   │   ├── Footer.astro       # links, socials, big "GRAND" wordmark
│   │   └── Logo.astro         # the recreated BJ shield + wordmark (SVG)
│   ├── pages/
│   │   └── index.astro        # the single page; assembles all components
│   └── styles/
│       └── global.css         # design tokens, resets, buttons, utilities
├── PRODUCT.md                 # brand, audience, voice, strategy
├── DESIGN.md                  # colors, type, layout decisions
├── astro.config.mjs
└── package.json
```

The page is assembled in [`src/pages/index.astro`](src/pages/index.astro);
reorder or remove sections there.

---

## Editing content (cheat sheet)

Most text and data lives in the "frontmatter" at the top of each component (the
part between the `---` fences). You don't need to touch the styling below it.

### 1. Contact details

**File:** [`src/components/Contact.astro`](src/components/Contact.astro) (top of file)

```js
const phoneDisplay = "+233 24 508 0252";        // shown on the page
const phoneHref    = "tel:+233245080252";        // Call button + tap-to-call
const whatsappHref = "https://wa.me/233245080252"; // WhatsApp button
const email        = "hello@bigjaddyent.com";    // ⚠️ placeholder, replace
```

Opening hours are a little lower in the same file (search for `Hours`), and they
also appear in [`src/components/Footer.astro`](src/components/Footer.astro).

> Phone numbers in `tel:` and WhatsApp links must use the international form
> (`+233…` / `233…`), not the local `0…` form.

### 2. Services, occasions, and gallery

Each of these is a simple list near the top of its component. Add, remove, or
edit items by changing the array.

| Section | File | Array |
|---------|------|-------|
| Service offerings | `src/components/Services.astro` | `services` |
| Occasion tiles | `src/components/Occasions.astro` | `occasions` |
| Gallery photos | `src/components/Gallery.astro` | `shots` |
| "About" highlights | `src/components/Intro.astro` | `highlights` |
| Nav links | `src/components/Header.astro` | `links` |
| Footer links / socials | `src/components/Footer.astro` | `explore`, `socials` |
| Form event types | `src/components/Contact.astro` | `eventTypes` |

Example, adding a service in `Services.astro`:

```js
const services = [
  // ...existing items...
  {
    t: "Valet Parking",
    d: "Stress-free arrivals with attended parking for your guests.",
    icon: `<path d="M4 17h16M6 17l1-5h10l1 5M8 12V9h8v3"/>`, // simple SVG path
  },
];
```

### 3. Images

Photos are loaded from Unsplash by ID. In each section you'll see a builder like:

```js
const src = (w) => `https://images.unsplash.com/photo-PHOTO_ID?auto=format&fit=crop&w=${w}&q=80`;
```

**To swap a photo:** replace the `PHOTO_ID` (the `1723832348105-2e69f948135a`
part of an Unsplash image URL).

**To use your own photos instead** (recommended before launch):

1. Put the file in `public/`, e.g. `public/images/hall.jpg`.
2. Reference it with a root-relative path: `src="/images/hall.jpg"`.
3. Keep the `width`/`height` attributes roughly matching the photo's real
   proportions so the layout doesn't jump while loading.

Always update the `alt` text to describe the new photo.

### 4. The logo

The mark is recreated as crisp SVG in
[`src/components/Logo.astro`](src/components/Logo.astro) (navy shield, gold rim,
skyline, "BJ"). It automatically switches color: white over the hero, navy once
the header turns solid.

If you have an official **transparent PNG/SVG** logo, drop it in `public/` and
replace the `<svg>…</svg>` block in `Logo.astro` with an `<img>` tag. The favicon
is a separate file: [`public/favicon.svg`](public/favicon.svg).

### 5. The inquiry form

In [`src/components/Contact.astro`](src/components/Contact.astro). On submit it
opens the visitor's email app with all the details pre-filled, addressed to the
`email` value, so **it works with no server**.

To collect submissions automatically instead, point the form at a service like
[Formspree](https://formspree.io/) or
[Netlify Forms](https://docs.netlify.com/forms/setup/): set the `<form>`'s
`action`/`method` and remove the `submit` handler script at the bottom of the
file.

### 6. The map

Also in `Contact.astro`:

```js
const mapQuery = "Hof Vilac International School, Achimota, Accra";
```

Change the text to move the pin. It uses Google Maps' free embed (no API key).

### 7. Colors and fonts

- **Colors** are CSS variables at the top of
  [`src/styles/global.css`](src/styles/global.css) (`--navy-*`, `--gold-*`,
  `--ivory`, etc.). Change them in one place and they update everywhere.
- **Fonts** are loaded in [`src/layouts/Layout.astro`](src/layouts/Layout.astro)
  (the Google Fonts `<link>`) and assigned via `--font-display` / `--font-body`
  in `global.css`.

See [DESIGN.md](DESIGN.md) for the full rationale and exact values.

---

## Design system

Two reference documents capture the thinking behind the site:

- **[PRODUCT.md](PRODUCT.md)** — who it's for, brand voice, what's offered, and
  the strategic principles.
- **[DESIGN.md](DESIGN.md)** — the navy + gold color tokens (OKLCH), typography,
  layout, motion, and imagery decisions.

In short: deep **navy** is the dominant brand color (hero, services, contact,
footer), **gold** is the accent, warm **ivory** carries the reading sections.
Type pairs an elegant Bodoni serif for headings with a clean grotesque for body.

---

## Before you launch (checklist)

- [ ] Replace the **email** placeholder (`hello@bigjaddyent.com`) in `Contact.astro` and `Footer.astro`
- [ ] Confirm or update the **opening hours** (`Contact.astro`, `Footer.astro`)
- [ ] Add real **social links** (Instagram / Facebook / TikTok are `#` placeholders in `Footer.astro`)
- [ ] Swap in your **own event photos** (see [Images](#3-images)) and update alt text
- [ ] Add the **official logo** file if you have one
- [ ] Decide how form submissions are handled (email app vs. Formspree/Netlify)
- [ ] Set your real domain in `astro.config.mjs` (`site:`) for correct link previews
- [ ] (Optional) wire the form to a backend if you want submissions stored

---

## Deployment

`npm run build` produces a fully static site in `dist/` that can be hosted
anywhere. Common options:

**Netlify / Vercel (recommended, free tier):**
- Connect the repo (or drag-and-drop the `dist/` folder on Netlify).
- Build command: `npm run build`
- Publish directory: `dist`

**Any static host (cPanel, S3, GitHub Pages, etc.):**
- Run `npm run build` and upload the contents of `dist/`.

Before deploying, set your domain in [`astro.config.mjs`](astro.config.mjs):

```js
export default defineConfig({
  site: 'https://your-domain.com',
  // ...
});
```

---

## Accessibility & performance

- Semantic HTML, a "skip to content" link, descriptive `alt` text, and visible
  focus styles.
- Honors `prefers-reduced-motion` (animations switch off for those users).
- Responsive images (`srcset`) and lazy loading for below-the-fold photos.
- No heavy JavaScript framework; the HTML + CSS payload is tiny. Hosting your
  own optimized images (instead of remote Unsplash) will make it even faster.

---

## Credits

- Built with [Astro](https://astro.build/).
- Fonts: [Libre Bodoni](https://fonts.google.com/specimen/Libre+Bodoni) and
  [Hanken Grotesk](https://fonts.google.com/specimen/Hanken+Grotesk) via Google Fonts.
- Placeholder photography from [Unsplash](https://unsplash.com/) (free for
  commercial use). Replace with your own venue photos for launch.

---

© BIG JADDY ENT. An arm of Big Jaddy Enterprise.
