# RouteLog

A financial dashboard for gig delivery workers — built by a Flex driver, for Flex drivers.

**Live app:** [robscode96.github.io/routelog](https://robscode96.github.io/routelog)

---

## What It Does

RouteLog treats every delivery block as a **route** — a single record that pairs earnings, mileage, and time together. Everything else flows from that: weekly and monthly progress, effective hourly rate, and a quarterly tax estimate that actually matches how the IRS works.

- **Log routes** in under 30 seconds — earnings, miles, start/end time, route type, notes
- **Dashboard** shows this week and this month: earnings vs. goal, miles, pace indicator, and hourly rate
- **Full history** with weekly grouping, text search, and filter by route type (Flex, DoorDash, etc.)
- **Quarterly tax view** — the feature that doesn't exist anywhere else. SE tax, federal income tax, and state income tax, broken down per quarter with IRS due dates and a downloadable summary
- **Settings** for income goals, IRS mileage rate, tax bracket, state rate, and custom route types
- **Google Sign-In** (Phase 2) — sync your data across devices via a self-hosted backend

---

## Why I Built This

Existing tools track income and mileage separately with no concept of a "route" as a single event. None of them show a clean quarterly breakdown with an estimated tax liability — which is what actually matters when you're a 1099 contractor making quarterly IRS payments.

---

## Privacy

- **Phase 1 (offline mode):** No accounts. No sign-in. No data collection. All data stays on your device via `localStorage`.
- **Phase 2 (signed in):** Data syncs to a self-hosted server on a Raspberry Pi. No third-party cloud. Your data never touches anyone else's infrastructure.

---

## Install as an App

RouteLog is a Progressive Web App — no App Store required.

**iPhone:** Tap the Share button → "Add to Home Screen"  
**Android:** Tap the browser menu → "Add to Home Screen"

---

## Tech Stack

**Frontend**
- Plain HTML, CSS, and JavaScript — no frameworks
- `localStorage` for offline/Phase 1 data storage
- Google Sign-In (OAuth 2.0) for Phase 2 auth
- Hosted on GitHub Pages

**Backend (Phase 2)**
- Python + Flask REST API
- PostgreSQL database
- Docker + Docker Compose
- Self-hosted on Raspberry Pi via Cloudflare Tunnel

---

## Project Structure

```
routelog/
├── index.html          # The entire frontend — one file
├── SCHEMA.md           # Canonical data schema (frontend + backend)
├── CHANGELOG.md        # Version history
├── docker-compose.yml  # Spins up API + database on the Pi
├── .env.example        # Environment variable template
├── .gitignore
└── backend/
    ├── app.py          # Flask API — auth, routes, settings, import
    ├── Dockerfile
    └── requirements.txt
```

---

## Roadmap

| Version | Scope |
|---------|-------|
| ✅ 1.0 | Flex Earnings Tracker (original) |
| ✅ 2.0 | RouteLog — full dashboard, tax view, PWA, Google Sign-In, backend API |
| 2.1 | Pi deployment, Cloudflare Tunnel |
| 2.2 | Quarterly email reminders |

---

*Built by a Flex driver in Oakland Township, Michigan.*
