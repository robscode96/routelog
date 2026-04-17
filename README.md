# RouteLog

A financial dashboard for gig delivery workers. Track earnings, mileage, and quarterly taxes — all on your device.

🔗 **Live app:** [robscode96.github.io/flex-tracker](https://robscode96.github.io/routelog)

---

## Features

- **Route logging** — log each delivery block in under 30 seconds: earnings, miles, start/end time, route type, and notes
- **Home dashboard** — weekly and monthly earnings vs. goals, pace tracking, miles driven, and effective hourly rate
- **Full history** — every route grouped by week, with live search and per-week totals
- **Quarterly tax estimates** — federal SE tax, federal income tax, and state income tax calculated per quarter with links to IRS Direct Pay and Michigan Treasury Online
- **PDF export** — print-ready quarterly tax summary for your records or tax preparer
- **Route editing** — correct any logged route after the fact
- **CSV export** — download all your data anytime

---

## Privacy

No accounts. No sign-in. No analytics. No servers.

All data is stored locally on your device using the browser's built-in storage. Nothing is ever transmitted anywhere.

---

## Installation

RouteLog is a Progressive Web App. No App Store required.

**iPhone:** Open the app in Safari → tap the Share icon → "Add to Home Screen"  
**Android:** Open in Chrome → tap the menu → "Add to Home Screen"

The app works fully offline after the first load.

---

## Tech Stack

| | |
|---|---|
| Language | HTML, CSS, JavaScript — no frameworks |
| Storage | Browser `localStorage` |
| Hosting | GitHub Pages |
| PWA | Service Worker + Web App Manifest |

---

## Running Locally

```bash
git clone https://github.com/obscode96/flex-tracker.git
open index.html
```

No build step. No dependencies. Open the file and it works.

---

## Project Files

```
├── index.html        — The application
├── PRODUCT_SPEC.md   — Product specification
├── CHANGELOG.md      — Version history
└── DEPLOY.md         — Deployment guide
```
