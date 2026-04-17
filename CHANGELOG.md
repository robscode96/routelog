# RouteLog — Changelog

All notable changes to this project are documented here.  
Format: [Version] — Date — Description

---

## [1.4.0] — 2026-04-16

### Added
- **History type filter chips** — filter route history by type (All / Flex / DSP / DoorDash / etc.) with scrollable chip row above the search bar
- **Improved app icon** — replaced plain "RL" text icon with a proper SVG icon for the PWA home screen shortcut

### Changed
- **PDF/tax export** — replaced clunky print dialog with a direct `.html` file download. Opens cleanly in any browser and prints to PDF from there. Filename format: `RouteLog-Q1-2026-Tax-Summary.html`
- **Tax export label** — "Michigan state income tax" → "State income tax" in downloaded summary
- Service worker cache bumped to `routelog-v1.4.0`
- Settings footer version bumped to v1.4.0

---

## [2.0.0] — 2026-04-16

### Added
- **Google Sign-In** — OAuth 2.0 authentication
- **Backend API** — Python/Flask REST API with full CRUD for routes and settings
- **PostgreSQL database** — persistent server-side storage (users, routes, settings tables)
- **Docker Compose** — deploys API + database together on the Pi
- **Automatic sync** — routes and settings push to server after every save/edit/delete
- **localStorage migration** — one-time import of existing local data on first sign-in
- **Offline fallback** — API_BASE = '' runs app in localStorage-only mode, no login required
- **Login screen** — shown when backend is configured and user is not authenticated
- **User badge** — shows signed-in name in home header; tap to sign out
- `.env.example` and `.gitignore`

---

## [1.3.0] — 2026-04-16

### Fixed
- "Michigan state tax" labels → "State income tax (X%)" in tax view and PDF export

### Added
- SCHEMA.md — canonical data schema
- CHANGELOG.md

---

## [1.2.6] — prior release

Full Phase 1 feature set: route logging, dashboard, history, quarterly tax view, PDF/CSV export, settings, onboarding, edit route, swipe-to-delete, PWA, service worker, bottom nav.

---

## Roadmap

| Version | Scope |
|---------|-------|
| 2.1.0 | Pi deployment, Cloudflare Tunnel |
| 2.2.0 | Quarterly email reminders |
