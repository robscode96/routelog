# RouteLog — Changelog

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
