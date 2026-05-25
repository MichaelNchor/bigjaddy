# DESIGN.md — BIG JADDY ENT Event Center

## Direction

Grand & Elegant. Deep navy is the dominant brand color (hero, CTA bands,
footer); gold is the accent that signals "grand"; warm ivory carries the
content sections. Sectional drench, not timid restraint. Color strategy:
**Committed** (navy carries large surfaces, gold ≈ accent, ivory = reading).

## Color (OKLCH)

Tinted neutrals toward the navy hue; never pure #000 / #fff.

| Token            | OKLCH                  | Use                                  |
|------------------|------------------------|--------------------------------------|
| `--navy-950`     | oklch(0.17 0.04 258)   | deepest navy, footer                 |
| `--navy-900`     | oklch(0.22 0.055 258)  | hero base, CTA band                  |
| `--navy-800`     | oklch(0.29 0.07 257)   | primary brand navy, buttons on light |
| `--navy-700`     | oklch(0.38 0.075 256)  | hovers, secondary navy               |
| `--gold-600`     | oklch(0.66 0.12 74)    | gold text on light surfaces          |
| `--gold-500`     | oklch(0.78 0.135 80)   | primary gold accent                  |
| `--gold-400`     | oklch(0.84 0.115 84)   | gold on navy, highlights             |
| `--gold-200`     | oklch(0.92 0.06 88)    | faint gold tints, rules              |
| `--ivory`        | oklch(0.975 0.008 85)  | page background (light sections)     |
| `--cream`        | oklch(0.955 0.012 84)  | alternating section background       |
| `--ink`          | oklch(0.26 0.025 262)  | body text on light                   |
| `--muted`        | oklch(0.50 0.02 262)   | secondary text on light              |
| `--line`         | oklch(0.89 0.012 262)  | hairline borders on light            |
| `--on-navy`      | oklch(0.96 0.012 86)   | text on navy                         |
| `--on-navy-soft` | oklch(0.82 0.02 250)   | secondary text on navy               |

## Typography

- **Display:** Libre Bodoni (Bodoni revival, Didone). Hero word, section titles,
  the gold italic "Grand." accent. Weights 400–700. Same elegant Bodoni
  character as Bodoni Moda but with sturdier strokes that stay legible at a
  distance (Bodoni Moda's optical hairlines receded on the hero). Hero headline
  runs at weight 700; section titles 700. Not the Playfair/Cinzel wedding reflex.
- **Body / UI:** Hanken Grotesk. All running text, nav, labels, buttons. Warm,
  legible grotesque. Weights 300–800.
- Two families, deliberately. Display serif + sans body = the luxury/editorial
  magazine shape that fits "grand."
- Fluid `clamp()` scale, ≥1.25 ratio between steps. Caps reserved for short
  tracked labels; never body copy. Do not put a tracked kicker above *every*
  section (avoid AI scaffolding); vary section openings.

## Layout

- Asymmetric, left-aligned compositions. No centered icon-title-text card stacks.
- Fluid spacing with `clamp()`; vary rhythm between sections.
- Occasion + gallery use real imagery in an editorial grid, not uniform cards.
- Content max width ~72rem; reading copy capped ~68ch.

## Logo

Faithful SVG recreation of the real logo: royal-blue shield with a gold rim and
inner hairline, the skyline breaking the top edge (rotunda + arcade, two towers,
a gear), the interlocked gold "BJ" monogram, and the hammer over the J. Colors
are self-contained (royal blue #2c63cc→#15397f, gold #ffe071→#ef9d1e) so the
mark reads on any background. Pairs with a "BIG JADDY / EVENT CENTER" wordmark
whose color flips (white over the hero, navy on the solid header). The favicon
is a simplified shield + BJ for legibility at tiny sizes. Swap in the official
vector if one becomes available.

## Motion

- Scroll-triggered staggered reveals (IntersectionObserver), ease-out, no bounce.
- Header transitions from transparent-on-hero to solid ivory when scrolled.
- Respect `prefers-reduced-motion`.

## Imagery

Authentic, warm Ghanaian / African celebration photography (Unsplash, verified
URLs). Hero: grand chandelier-lit reception hall. Navy gradient overlay on the
hero so gold/ivory type stays legible.
