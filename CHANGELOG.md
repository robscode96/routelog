# Changelog

All notable changes to RouteLog are documented here.  
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).  
Versioning follows [Semantic Versioning](https://semver.org/): MAJOR.MINOR.PATCH

---

## [1.2.6] — 2026-04-16

### Changed
- Pace badges restored to filled style (green/amber for goal badge, dark fill for time badge).

---

## [1.2.5] — 2026-04-16

### Fixed
- Pace badges no longer wrap awkwardly next to the earnings amount. Text is now `nowrap` and centered within each badge.

---

## [1.2.4] — 2026-04-16

### Changed
- Pace badges now use outline style instead of filled background — cleaner look
- "% of time" label now reads "% of week" or "% of month" depending on context

---

## [1.2.3] — 2026-04-16

### Added
- Second pace bubble on Home showing how far through the current week or month you are (e.g. "60% of time"). Sits next to the goal percentage badge so you can instantly compare earnings progress vs. time elapsed.

---

## [1.2.2] — 2026-04-16

### Changed
- Pace badges on Home now show percentage of goal reached (e.g. "63% of goal") instead of dollar amount ahead/behind. Green when on pace, amber when behind.

---

## [1.2.1] — 2026-04-16

### Fixed
- Pace badges (ahead/behind) no longer show on Home when no routes have been logged for that week or month. Previously the app would calculate a deficit against the goal even with $0 earned and no activity, which was misleading on a fresh install.

---

## [1.2.0] — 2026-04-16

### Added
- **Onboarding flow** — first-run setup screen collects weekly/monthly income goals, federal tax bracket, and state tax rate before the user logs their first route. Pre-filled with Michigan defaults. Skippable.
- **Edit route** — routes can now be edited from the History detail sheet. All fields (earnings, miles, date, times, type, notes) are editable. Changes reflect immediately across Home and History.
- **PWA manifest** — inline web app manifest enables proper "Add to Home Screen" behavior with RouteLog branding on iOS and Android.
- **Service worker** — app now caches itself for full offline use after first load. Works in a parking lot with no signal.
- **GitHub Pages deploy guide** — `DEPLOY.md` added with step-by-step instructions for publishing to a live URL and sharing with coworkers.

### Changed
- Route detail sheet now has three actions: Close, Edit, Delete (previously just Close and Delete)

---

## [1.1.0] — 2026-04-16

### Added
- **History view** — fifth nav tab showing all routes ever logged, grouped by week with week-total headers. Includes lifetime stats bar (total earnings, miles, block count, avg per block) and live search filtering by date, type, notes, or amount.
- **Quarterly PDF export** — each quarter in the Tax view now has an "Export PDF summary" button. Opens a print-ready page with full tax breakdown, route detail table, payment due date, and links to IRS Direct Pay and Michigan MTO.
- **Route detail sheet** — tapping any route in History slides up a detail panel showing earnings, miles, duration, effective hourly rate, and notes. Includes Delete action.
- **State income tax** — Tax view now calculates and displays Michigan state income tax (or any configurable flat rate) alongside federal estimates. State tax rate is user-configurable in Settings (default: 4.25% Michigan).
- **Michigan MTO link** — Tax view links directly to Michigan Treasury Online for state estimated payments alongside the existing IRS Direct Pay link.
- **Swipe-to-delete** — routes in Home and History can be swiped left to reveal a delete button. Rebuilt on Pointer Events API for reliable cross-device behavior.

### Changed
- Tax calculation now correctly applies the SE tax deduction to both federal and state taxable income bases
- Settings page updated with state tax rate field
- "Total estimated payment due" in Tax view now reflects federal SE tax + federal income tax + state income tax combined
- Version footer updated

### Fixed
- Swipe gesture no longer accidentally triggers route tap/detail actions
- Delete from History now re-renders History (previously re-rendered Home)

---

## [1.0.0] — 2026-04-16

### Added
- **Route logging** — log earnings, mileage, date, start/end time, route type, and notes. Designed to complete in under 30 seconds with large tap targets and numeric keyboards.
- **Home dashboard** — weekly and monthly earnings vs. goals with animated progress bars, pace badges (ahead/behind based on time elapsed), miles totals for week and month, effective hourly rate when times are logged, and recent 7 routes list.
- **Quarterly tax view** — all four quarters for the current year, each showing: earnings, miles, mileage deduction, SE tax deduction, net taxable income, self-employment tax, federal income tax, and total estimated payment due. Current quarter opens automatically. Links to IRS Direct Pay.
- **Settings** — weekly/monthly income goals, IRS mileage rate (default: 70¢/mi), federal tax bracket selector, custom route types (add/remove), CSV export of all routes, and full data reset with confirmation.
- **CSV export** — exports all routes to a downloadable spreadsheet.
- **Delete route** — routes deletable from Home recent list via swipe-to-reveal or trash button, with confirmation modal.
- **localStorage persistence** — all data stored on-device. No account, no server, no data collection.
- Weeks start on Sunday, matching the Amazon Flex pay cycle.

---

## Roadmap

### Planned — Phase 2
- Multi-user support with self-hosted backend
- PostgreSQL/SQLite database per user
- Email or Google Sign-In authentication
- Hosting via Cloudflare Tunnel (Starlink CGNAT bypass)

### Planned — Phase 2.1
- Quarterly email reminders before IRS/state due dates
- Enhanced PDF export options
