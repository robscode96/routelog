# RouteLog — Changelog

All notable changes to this project are documented here.  
Format: [Version] — Date — Description

---

## [2.0.0] — 2026-04-16

### Added
- **Google Sign-In** — users authenticate with their Google account via OAuth 2.0
- **Backend API** — Python/Flask REST API (`backend/app.py`) with full CRUD for routes and settings
- **PostgreSQL database** — persistent server-side storage with `users`, `routes`, and `settings` tables
- **Docker Compose** — `docker-compose.yml` spins up the API and database together on the Pi
- **Automatic sync** — routes and settings push to the server in the background after every save/edit/delete
- **localStorage migration** — one-time import of existing local data to the server account on first login
- **Offline fallback** — if `API_BASE` is empty, the app runs in localStorage-only mode (no login required)
- **Login screen** — clean sign-in UI shown when backend is configured and user is not authenticated
- **User badge** — shows signed-in user's name in the home header; tap to sign out
- `.env.example` — environment variable template for Pi deployment
- `.gitignore` — prevents secrets from being committed

### Changed
- Service worker cache bumped to `routelog-v1.3.0`

---

## [1.3.0] — 2026-04-16

### Fixed
- **Tax view and PDF export:** Removed hardcoded "Michigan state tax" labels. Now displays as "State income tax (X%)" so the app works correctly for drivers in any state.

### Added
- **SCHEMA.md:** Canonical data schema document
- **CHANGELOG.md:** This file

---

## [1.2.6] — (prior release)

### Summary
Full Phase 1 feature-complete release. Route logging, dashboard, history, quarterly tax view, PDF export, CSV export, settings, onboarding, edit route, PWA manifest, service worker, bottom nav.

---

## Roadmap

| Version | Scope |
|---------|-------|
| 2.0.x | Pi deployment, Cloudflare Tunnel setup |
| 2.1.0 | PDF export improvements, quarterly email reminders |


All notable changes to this project are documented here.  
Format: [Version] — Date — Description

---

## [1.3.0] — 2026-04-16

### Fixed
- **Tax view and PDF export:** Removed hardcoded "Michigan state tax" labels. Now displays as "State income tax (X%)" so the app works correctly for drivers in any state.

### Added
- **SCHEMA.md:** Canonical data schema document defining the Route object, Settings object, localStorage keys, IRS quarter definitions, tax calculation logic, and the planned Phase 2 backend database tables. This is the source of truth for all data structures going forward.
- **CHANGELOG.md:** This file. All future changes will be logged here.

---

## [1.2.6] — (prior release)

### Summary
Full Phase 1 feature-complete release. Includes:
- Route logging (earnings, miles, start/end time, route type, notes)
- Dashboard with weekly/monthly earnings progress, miles, pace indicators, and effective hourly rate
- Full route history with weekly grouping, search, and swipe-to-delete
- Quarterly tax view with IRS-accurate estimates (SE tax, federal income, state income, mileage deduction)
- PDF export per quarter
- CSV export of all routes
- Settings (goals, mileage rate, tax bracket, state rate, custom route types)
- Onboarding flow
- Edit route sheet
- PWA manifest for home screen installation
- Service worker for offline access
- Bottom navigation bar

---

## Roadmap

| Version | Scope |
|---------|-------|
| 1.3.x | Bug fixes, Phase 1 polish |
| 2.0.0 | Backend (Python/Flask), PostgreSQL, Google Sign-In, multi-device sync |
| 2.1.0 | PDF export improvements, quarterly email reminders |
