# Dette Portal — Client Portal (Dom Design Studio)

## What this is

A static client portal for a **Houston, TX** studio that handles weddings,
real-estate listings, and special events. Plain **HTML / CSS / JS**, hosted on
**GitHub Pages**. No build step, no framework, no bundler.

## Audience & voice

- Client and end users are **US, English**. Houston, TX (Central time).
- Use US formats: AM/PM times, "Month D, YYYY" dates. **No bilingual / French.**
- Tone: confident, editorial, understated. No marketing fluff.

## Brand & design system  (source of truth = `css/style.css`)

- **Palette:** ink `#1A1714`, ivory `#FAF7F2`, paper `#FFFFFF`,
  terracotta accent `#9A6A4F` (soft `#F1E9DE`), hairline `#D9CFC2`, mute `#6B6258`.
  Category tints: rose (weddings), sage (real estate), sand (special events).
- **Type:** Gloock (display headings), Italiana (wordmark / accent),
  Instrument Sans (body), Geist Mono (eyebrows, labels, numerals).
  Fonts are bundled in `assets/fonts/` — do NOT swap to Google Fonts.
- **Aesthetic:** Swiss / editorial minimalism — 2px radius, hairline borders,
  uppercase mono eyebrows with wide letter-spacing, generous whitespace, restraint.

## File structure

```
index.html          login page
dashboard.html      Step 01 — calendar dashboard (month grid + event list)
add-event.html      Step 02 — add to calendar form
emergency.html      Step 03 — address book / emergency contacts
shop.html           Step 04 — 2027 calendar pre-order shop
css/style.css       design system + all shared styles (SOURCE OF TRUTH — reuse before adding)
js/app.js           shared logic: sidebar nav render, toast utility, DOMContentLoaded init
assets/fonts/*      bundled typefaces
```

## Conventions

- **Reuse existing `style.css` classes** (`.sidebar`, `.panel`, `.chip`,
  `.event-row`, `.toast`, `.btn`) before inventing new ones. Net-new styles go
  in `css/style.css`, never overwrite the system.
- **`js/app.js` is the single shared script** — it renders the sidebar nav on
  every inner page via `renderSidebar()` and exposes `showToast()`. Link it in
  every page except `index.html`.
- **Vanilla JS, no heavy deps.** If a real calendar is needed, the chosen libs
  are FullCalendar (MIT core) for the grid, Alpine for interactivity, GSAP for
  motion — all via CDN, still no build step.
- **Icons:** inline SVG, Lucide-style (24 grid, 2px round stroke).
- **Accessibility:** visible `:focus-visible`, real `<button>`s for controls,
  Esc closes the drawer, honour `prefers-reduced-motion`.

## Status

- **Done:** login (`index.html`); four-step inner portal — dashboard
  (`dashboard.html`), add-to-calendar form (`add-event.html`), address book
  (`emergency.html`), and shop (`shop.html`). Shared sidebar nav is rendered
  by `js/app.js` from the `NAV_ITEMS` array.
- **Next:** wire live event data into `dashboard.html`; replace placeholder
  brokerage / venue names; optionally swap the hand-built calendar grid for
  FullCalendar for real month-to-month navigation.

## Gotchas

- The calendar in `dashboard.html` is a static demo — prev/next are not yet
  wired to real date logic. Replace when adding live data.
- Brokerage names (Compass, Keller Williams) and venues are **placeholders** —
  swap for the client's actual firms before presenting.
- The sidebar nav is driven by the `NAV_ITEMS` array at the top of `js/app.js`.
  Add or reorder pages there.
