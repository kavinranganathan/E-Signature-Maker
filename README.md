# E-Signature Maker

A single-page web app to create a signature by **drawing** it on a canvas or **typing** it in a handwriting font, then download it as **PNG**, **JPG**, or **PDF**. Everything runs client-side — no server, no build step, no dependencies to install. Your signature never leaves the browser.

## Features

- **Draw mode** — smooth canvas drawing (quadratic curves), mouse + touch, pen color (black/blue/red) and thickness.
- **Type mode** — 5 Google handwriting fonts (Caveat, Pacifico, Dancing Script, Great Vibes, Allura), text color and size.
- **Controls** — Clear, Undo (per stroke), transparent/white background toggle, live preview.
- **Download** — pick a format (PNG keeps transparency, JPG forces white, PDF centers on A4) and click Download. Files are named `signature.png` / `.jpg` / `.pdf`.
- Fixed 600×200 export resolution (rendered at 2–3× for crisp output).

## Run locally

It's a static file — just open it:

```bash
open index.html        # macOS
```

Or serve it (recommended, so Google Fonts and jsPDF load over http):

```bash
npx serve .            # then visit the printed URL
```

## Deploy to Vercel

This repo is a zero-config static site. Vercel serves `index.html` directly.

**Via the dashboard:** import the repo at [vercel.com/new](https://vercel.com/new) — no settings to change. Framework Preset: **Other**.

**Via the CLI:**

```bash
npm i -g vercel        # if you don't have it
vercel                 # preview deployment
vercel --prod          # production deployment
```

[`vercel.json`](./vercel.json) sets `framework: null` (pure static, no build), clean URLs, basic security headers, and tells the CDN to always revalidate `index.html` so updates show immediately.

## Project structure

```
.
├── index.html     # the entire app (HTML + CSS + JS inline)
├── vercel.json    # static deploy config
├── README.md
└── .gitignore
```

External resources are loaded from CDNs at runtime: Google Fonts (handwriting fonts) and [jsPDF](https://github.com/parallax/jsPDF) (PDF export). An internet connection is required for typed fonts and PDF export.

## Analytics

[Vercel Web Analytics](https://vercel.com/docs/analytics) is wired in via the static-site script snippet at the bottom of `index.html` (this is a vanilla HTML app, so the `@vercel/analytics` React component / `npm install` is not used). To start collecting page views:

1. Deploy the project to Vercel.
2. In the Vercel dashboard, open the project → **Analytics** tab → **Enable**.

Vercel then serves `/_vercel/insights/script.js` automatically and data appears in that tab. The script is a no-op when running locally or on non-Vercel hosts, so it's safe to leave in.
