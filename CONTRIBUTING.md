# Contributing to Memory Frame LP

Thanks for offering to help. The site is a single static `index.html` (no build step), but two integrations need real backend / vendor accounts.

If you can pick up either of the open tasks below, please **open a GitHub issue first** to align on approach before coding — there are usually 2–3 reasonable architectures for each.

---

## 🟢 Open task #1 — Stripe ($1 reservation hold)

### Current state
- Reservation form is in Section 9 (`Final CTA`, ID `#reserve` in `index.html`)
- Form action handler is a TODO — currently does nothing on submit
- Three pricing SKUs in Section 7:
  - `For Mom` — $399 (10″)
  - `For Both Sides` — $729 (two 10″)
  - `For the Family Wall` — $699 (15″ Premium)

### What needs to happen
1. **Frontend**: replace form submit with Stripe Checkout (recommended) or Payment Element
2. **Backend (serverless function)**: create a Stripe Checkout Session, return URL to client
3. **Webhook**: handle `payment_intent.succeeded` / `checkout.session.completed`
4. **Charge model**: authorize $1 only at reservation time. Full price ($399–$729) is charged later, manually, when ship date is confirmed by email. (See "Honesty constraints" below.)
5. **Storage**: persist reservation — email + SKU + timestamp. Lightweight (Airtable / Notion / D1 / Supabase) is fine.

### Suggested stack
- Vercel or Netlify Functions (serverless, free tier covers pre-launch volume)
- Stripe Checkout (link-based, lowest friction)

### Secrets needed (don't commit — see `.env.example`)
- `STRIPE_PUBLISHABLE_KEY` — frontend OK to expose, but read from env
- `STRIPE_SECRET_KEY` — backend only
- `STRIPE_WEBHOOK_SECRET` — backend only

---

## 🟢 Open task #2 — ESP (email service for waitlist + receipts)

### Current state
- "Join the waitlist" link below the reservation form is a placeholder (no destination)
- No email is sent on reservation
- No transactional templates exist yet

### What needs to happen
1. **Pick an ESP**: recommend **Loops** or **Resend** for transactional. Postmark is a strong alternative.
2. **Two flows**:
   - **Waitlist**: collects email only, no $1. Sends "you're on the list, we'll email when reservations widen."
   - **Reservation**: triggered by Stripe webhook (task #1). Sends "your $1 is held. We'll email you 5 days before charging full price when your ship date is confirmed."
3. **Templates**: cream background, italic serif headlines, body in light Barlow. Founder voice — see Section 6 (`Mira`) in `index.html` for tone reference.

### Secrets needed (don't commit — see `.env.example`)
- `ESP_API_KEY`
- `ESP_PROVIDER` (e.g. `loops`, `resend`, `postmark`)

---

## How to work

1. **Open an issue first** — describe your proposed approach and ask any clarifying questions.
2. **Fork** the repo and create a branch (e.g. `feat/stripe-checkout`).
3. **Test locally**: `python3 -m http.server 8765` from the repo root.
4. **PR to `main`**. Vercel/Netlify previews (if configured) will give you a public preview URL.

## Honesty constraints — don't undo these

- ❌ Don't promise specific ship dates ("ships May 2026", "in time for Mother's Day"). Use: *"Ship date confirmed by email before your card is charged."*
- ❌ Don't add fake testimonials. Pre-launch — there are none yet.
- ❌ Don't add Google Analytics, Facebook Pixel, or any third-party tracking before discussing. The brand is *on-device AI / no cloud / no telemetry* — uninstrumented LP is fine for pre-launch.
- ❌ Never commit secrets. Always use env vars + `.env.example`.

## Need to reach Shayla?

Open a GitHub issue. For sensitive coordination (Stripe account creation, domain DNS, etc.), email is in the LP footer.
