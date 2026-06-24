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
index.html          login page — role-aware sign-in/register routing
dashboard.html      generic Step 01 — calendar dashboard (month grid + event list)
add-event.html      generic Step 02 — add to calendar form
emergency.html      generic Step 03 — address book / emergency contacts
shop.html           generic Step 04 — 2027 calendar pre-order shop
wedding/*.html      Wedding Portal — category-specific clone of the four steps above
                     (dark sidebar theme, wedding-only content), reachable when a
                     "Wedding client" signs in
css/style.css       design system + all shared styles (SOURCE OF TRUTH — reuse before adding)
js/app.js           shared logic: sidebar nav render, toast utility, DOMContentLoaded init
assets/fonts/*      bundled typefaces
```

## Conventions

- **Reuse existing `style.css` classes** (`.sidebar`, `.panel`, `.chip`,
  `.event-row`, `.toast`, `.btn`) before inventing new ones. Net-new styles go
  in `css/style.css`, never overwrite the system.
- **`js/app.js` is the single shared script** — it renders the sidebar nav on
  every root-level inner page via `renderSidebar()` and exposes `showToast()`.
  Link it in every page except `index.html`.
- **Category portals (e.g. `wedding/`) own their own sidebar nav.** They still
  load `js/app.js` for `showToast()`, but define their own `WEDDING_NAV_ITEMS` /
  `renderWeddingSidebar()` under different names — `app.js` already declares
  `const NAV_ITEMS` and `function renderSidebar` at the top level, so a same-named
  redeclaration in an inline `<script>` throws `SyntaxError: Identifier has already
  been declared` and silently kills that whole script block. Page-specific theming
  (e.g. the wedding dark sidebar) goes in `css/style.css` scoped under a body class
  like `.wedding-theme`, not in inline `<style>` blocks.
- **Vanilla JS, no heavy deps.** If a real calendar is needed, the chosen libs
  are FullCalendar (MIT core) for the grid, Alpine for interactivity, GSAP for
  motion — all via CDN, still no build step.
- **Icons:** inline SVG, Lucide-style (24 grid, 2px round stroke).
- **Accessibility:** visible `:focus-visible`, real `<button>`s for controls,
  Esc closes the drawer, honour `prefers-reduced-motion`.

## Status

- **Done:** login (`index.html`) with role-aware routing — selecting "Wedding
  client" on Sign in / Create account sends users to `wedding/dashboard.html`,
  every other role goes to the generic `dashboard.html`; generic four-step inner
  portal (`dashboard.html`, `add-event.html`, `emergency.html`, `shop.html`); a
  parallel Wedding Portal under `wedding/` with its own dark-themed sidebar and
  wedding-only content. Shared sidebar nav on the generic pages is rendered by
  `js/app.js` from the `NAV_ITEMS` array.
- **Next:** wire live event data into `dashboard.html`; replace placeholder
  brokerage / venue names; build out Real Estate and Special Event portals
  alongside `wedding/` following the same pattern; optionally swap the
  hand-built calendar grid for FullCalendar for real month-to-month navigation.

## Gotchas

- The calendars in `dashboard.html` and `wedding/dashboard.html` are static
  demos — prev/next are not yet wired to real date logic. Replace when adding
  live data.
- Brokerage names (Compass, Keller Williams) and venues are **placeholders** —
  swap for the client's actual firms before presenting.
- The sidebar nav on generic pages is driven by the `NAV_ITEMS` array at the
  top of `js/app.js`. Add or reorder pages there. The `wedding/` portal has its
  own `WEDDING_NAV_ITEMS` array duplicated in each of its four files — update
  all four together when changing wedding nav.
