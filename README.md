# D'Ette Services — Portal Demo (Phase 0 Prototype)

A clickable, static prototype of the client portal described in the discovery
call (10 June 2026). Built to be **shown**, not to function — no real
authentication, no real Google Calendar connection, no real checkout.

## What's here

| Page | Purpose |
|---|---|
| `index.html` | Sign in / create account (gated entry point) |
| `dashboard.html` | Main portal: calendar + upcoming events + quick links |
| `add-event.html` | "Add to calendar" flow — shows the categorise → sync → route concept |
| `emergency.html` | Address book: emergency contacts, personal contacts, vendor directory |
| `shop.html` | 2027 calendar pre-orders + wedding merch (tees) |

All pages share `css/style.css` (brand tokens + components) and
`js/app.js` (sidebar nav + toast notifications).

## Brand tokens

Defined as CSS custom properties at the top of `css/style.css`:

- `--ink` `#1A1714` — primary text / sidebar
- `--ivory` `#FAF7F2` — page background
- `--accent` `#9A6A4F` — terracotta-taupe accent
- `--accent-soft` / `--rose` / `--sage` / `--sand` — category tint colours
- `--hairline` `#D9CFC2` — borders/dividers

Type: **Gloock** (display/headings), **Italiana** (wordmark/accents),
**Instrument Sans** (body/UI), **Geist Mono** (labels, tags, timestamps).

## What's mocked vs. real

- **Sign in / register** — any input logs you into the dashboard. No backend.
- **"Add to calendar"** — shows a toast confirmation only. No Google API call.
- **Shop "Add" buttons** — show a toast only. No cart/checkout.
- **Calendar dots** — static, hand-placed for the demo month (June 2026).

## Notes for the next build phase

- Real Google Calendar sync = OAuth consent screen + Calendar API write access.
  This is the one piece of genuine custom development — scope and price it
  separately.
- Confirm with the client what her offshore team's website build already
  covers, so this portal doesn't duplicate it.
- Shop section is designed to link out to Shopify rather than run its own
  cart in the real build.

## Running locally

No build step — open `index.html` directly, or serve the folder:

```bash
python3 -m http.server 8080
```

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. Repo Settings → Pages → Source: `main` branch, `/ (root)`.
3. Demo link will be `https://<username>.github.io/<repo-name>/`.
