# Memory Frame — Landing Page

Pre-launch landing page for **Memory Frame**, a wood-framed AI photo display, by **Mira**.

**Status**: Pre-launch · Accepting $1 refundable reservations · Ship date confirmed by email before charge.

**Live**: https://shayla-suen.github.io/Mira/ *(once GitHub Pages is enabled — placeholder; replace with your actual GitHub username path)*

---

## What this is

A single-file React landing page using Babel standalone (no build step). Drop into any static host.

- 10 sections: Hero (auto-loop video) → Intro → Capabilities (5-card carousel) → Problem → Thinking of You → Mira → Pricing → FAQ → Final CTA → Footer
- Cream / dark alternating theme
- All AI runs on-device — page reflects that (no app, no cloud, no subscription)

## Run locally

```bash
python3 -m http.server 8765
# open http://localhost:8765/
```

## Stack

- React 18 + Framer Motion (CDN)
- Tailwind CSS (CDN)
- Babel standalone (in-browser JSX compile)
- Plain HTML5 `<video>` for hero (`memory_frame_demo.mp4`)

No build step. No bundler. One file.

## Want to help?

Two open tasks need a developer who can wire up backend services. See **[CONTRIBUTING.md](CONTRIBUTING.md)**.

- 💳 **Stripe** — accept $1 reservation hold + ship-date-confirm flow
- 📧 **ESP** — waitlist confirmation + reservation receipts

## Brand

Made by **Mira** — a small studio that watched their own parents put a frame face-down.
