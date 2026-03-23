# Daily Brief

> A personal intelligence briefing agent — newspaper-style daily digest powered by Claude AI and live web search.

**[→ Open the app](https://securityguidebook.github.io/daily-brief)**

---

## What it does

Daily Brief generates a personalised morning and evening news digest across topics you care about. Each edition includes:

- **Topic sections** — 2–3 high-signal stories per topic with summaries and a "why it matters" line
- **TLDR News Roundup** — automatically pulls coverage from TLDR News Global and TLDR News EU
- **Worth watching** — 2–3 slow-burn developments to track across the week

Runs automatically at **6:00 AM** and **5:00 PM NZT** via a Cloudflare Worker cron. Can also be triggered on demand from the app.

## Features

- Toggle topics on/off — Cybersecurity, AI & ML, Geopolitics, Tech industry, Science, Markets, NZ news, AU news
- Add custom topics or keywords (e.g. "threat intelligence", "SIEM")
- Three depth settings — Headline, Standard, Deep Dive
- TLDR News Global and EU integration — no copy-pasting required
- Exclude topics you don't want
- Optional personal context to tailor the "why it matters" angle

## Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML/CSS/JS — no build step |
| Hosting | GitHub Pages |
| Backend | [daily-brief-worker](https://github.com/securityguidebook/daily-brief-worker) (Cloudflare Worker) |
| AI | Anthropic Claude Sonnet + web search |

## Setup

This frontend requires the [daily-brief-worker](https://github.com/securityguidebook/daily-brief-worker) to be deployed first.

Once the Worker is live, update this line in `daily-briefing-agent.html`:

```js
const WORKER_URL = 'https://daily-brief-worker.YOUR_NAME.workers.dev';
```

Then push to this repo and enable GitHub Pages:
`Settings → Pages → Deploy from branch → main → / (root)`

Your app will be live at `https://securityguidebook.github.io/daily-brief`.

## Daily Digivolve

The backend Worker exposes a `GET /brief` endpoint that returns the latest cached brief as JSON — including a pre-formatted `summary` string for the Daily Digivolve avatar to speak on startup. No changes needed to this frontend when that integration is added.

See [daily-digivolve](https://github.com/securityguidebook/daily-digivolve) for details.

## Security

All API calls go through the Cloudflare Worker — the Anthropic API key is never exposed in this frontend or stored in the browser.

## Related repos

- [daily-brief-worker](https://github.com/securityguidebook/daily-brief-worker) — Cloudflare Worker backend
- [daily-digivolve](https://github.com/securityguidebook/daily-digivolve) — avatar productivity companion (future integration)

---

*Part of the [securityguidebook](https://github.com/securityguidebook) portfolio.*
