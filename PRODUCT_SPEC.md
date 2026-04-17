# RouteLog — Product Specification

**A Financial Dashboard for Gig Delivery Workers**

| | |
|---|---|
| **Version** | 1.1 (Single-User) |
| **Author** | Robert |
| **Status** | Phase 1 Complete |
| **Updated** | 2026-04-16 |

---

## Problem Statement

Gig delivery workers — particularly Amazon Flex drivers — are 1099 independent contractors responsible for tracking their own earnings, mileage, and quarterly taxes. Existing tools fall short in key ways:

- **Stride** tracks income and mileage separately, with no way to pair a specific route's earnings to that route's mileage. There is no concept of a "route" as a single event.
- **Stride and similar apps** show yearly summaries only — but the IRS requires quarterly estimated tax payments (due in April, June, September, and January). No tool surfaces a clean quarterly breakdown with an estimated tax liability.
- **No tool accounts for state income tax** alongside federal taxes — leaving drivers to calculate state quarterly payments manually.
- **No single view** shows what you earned, how far you drove, what you owe the IRS and your state this quarter, and how you're tracking toward your income goals.

RouteLog solves all of this.

---

## Product Overview

RouteLog is a Progressive Web App (PWA) — a mobile-first web application that can be installed on a phone's home screen and used like a native app, with no App Store required. It is designed to be opened quickly between delivery routes, with fast data entry and clear at-a-glance summaries.

The core data unit is the **route**: a single delivery block that pairs earnings and mileage together as one record. All summaries, goals, and tax estimates are derived from route data.

---

## Target User

Amazon Flex drivers and other gig delivery workers (DoorDash, Instacart, etc.) who:

- Are 1099 independent contractors
- Track mileage manually (via Stride or odometer)
- Need to pay quarterly estimated taxes to the IRS and their state
- Want to track progress toward weekly and monthly income goals

---

## Core Features

### 1. Route Logging

The primary interaction. Designed to be completed in under 30 seconds.

**Fields:**
- Date (defaults to today)
- Earnings ($)
- Mileage (manual entry)
- Duration (optional — start/end time)
- Route type (Flex, DSP, other — user-configurable)
- Notes (optional)

**Behavior:**
- Large tap targets optimized for mobile
- Numeric keyboards auto-open for dollar and mileage fields
- Confirmation on save, then returns to dashboard

---

### 2. Dashboard (Home)

At-a-glance view of current performance.

**Displays:**
- This week's earnings vs. weekly goal (progress bar)
- This month's earnings vs. monthly goal (progress bar)
- Pace badges — ahead or behind based on time elapsed through the week/month
- Total miles this week / this month
- Effective hourly rate this week (if duration is logged)
- Recent routes list (last 7 entries, newest first)

---

### 3. Route History

Full scrollable log of all routes ever recorded.

**Features:**
- Grouped by week with per-week earnings and mileage totals
- Live search filtering by date, type, notes, or earnings amount
- Lifetime stats bar: total earnings, total miles, block count, average per block
- Tap any route to view full detail (earnings, miles, duration, rate, notes)
- Edit any route field after the fact
- Swipe left to delete; detail sheet also includes Delete action

---

### 4. Quarterly Tax View

The feature that doesn't exist anywhere else — covering both federal and state tax obligations.

**Displays per quarter (Q1–Q4):**
- Total earnings for the quarter
- Total miles for the quarter
- Estimated mileage deduction (miles × IRS standard rate)
- SE tax deduction (½ of self-employment tax — deductible from both federal and state taxable income)
- Net taxable income (earnings − mileage deduction − SE deduction)
- Estimated self-employment tax owed (15.3% of net × 92.35%)
- Estimated federal income tax owed (user's bracket — configurable in Settings)
- **Estimated state income tax owed** (net taxable income × state rate — configurable, default 4.25% Michigan)
- Total estimated payment due (all three combined)
- IRS payment due date for that quarter
- Link to IRS Direct Pay
- Link to Michigan Treasury Online (MTO)
- PDF export of full quarterly summary

**Quarter date ranges:**

| Quarter | Earnings Period | Federal Due | State Due |
|---|---|---|---|
| Q1 | Jan 1 – Mar 31 | April 15 | April 15 |
| Q2 | Apr 1 – May 31 | June 15 | June 15 |
| Q3 | Jun 1 – Aug 31 | September 15 | September 15 |
| Q4 | Sep 1 – Dec 31 | January 15 (next yr) | January 15 (next yr) |

**Tax calculation order (matters for accuracy):**
1. Calculate gross SE tax (net earnings × 92.35% × 15.3%)
2. SE deduction = gross SE tax ÷ 2 (deductible from both federal and state bases)
3. Net taxable income = earnings − mileage deduction − SE deduction
4. Federal income tax = net taxable income × bracket rate
5. State income tax = net taxable income × state rate
6. Total due = SE tax + federal income tax + state income tax

> **Note:** Progressive-bracket states (e.g. California, New York) are not modeled precisely — the flat-rate field gives a reasonable estimate. Bracket-based state tax support is a future enhancement.

---

### 5. Settings

User-configurable preferences that make the app work for anyone, not just one person.

**Options:**
- Weekly earnings goal ($)
- Monthly earnings goal ($)
- IRS standard mileage rate (pre-filled with current rate, user can override)
- Federal income tax bracket (dropdown: 10%, 12%, 22%, 24%, 32%, 35%, 37%)
- **State income tax rate (%)** — pre-filled with 4.25% for Michigan; user can override for any state
- Route types (add/remove custom labels)
- Data export (full CSV of all routes)
- Data reset

---

## Navigation

Bottom navigation bar — always visible, thumb-accessible:

```
[ Home ]  [ History ]  [ + Log ]  [ Tax ]  [ Settings ]
```

No hamburger menu. No hidden navigation. The five core sections are always one tap away. Log is center-positioned and visually elevated — it's the primary action.

---

## Onboarding

First-run setup screen shown to new users before they log their first route. Collects:
- Weekly and monthly income goals
- Federal tax bracket
- State income tax rate

Pre-filled with Michigan defaults. Skippable. Never shown again after completion.

---

## Technical Architecture

### Phase 1 — Single User (current)

| Layer | Technology |
|---|---|
| Frontend | Single-page HTML/CSS/JavaScript (no framework) |
| Storage | Browser `localStorage` — all data on-device |
| Hosting | GitHub Pages (free, static) |
| PWA | Service worker + Web App Manifest (inline, single-file) |
| Fonts | Space Mono + DM Sans via Google Fonts |

No account required. No data leaves the device.

### Phase 2 — Multi-User (planned)

| Layer | Technology |
|---|---|
| Backend | Node.js + Express or Python + Flask |
| Database | PostgreSQL or SQLite |
| Auth | Email/password or Google Sign-In |
| Hosting | Self-hosted via Cloudflare Tunnel (bypasses Starlink CGNAT) |

Each user's data isolated under their own account.

---

## Design Principles

1. **Fast first.** Log Route must be completable in under 30 seconds.
2. **Mobile first.** Designed for a phone screen, used in a parking lot between blocks.
3. **No noise.** Only show what matters. No ads, no upsells, no onboarding friction.
4. **Your data is yours.** Phase 1 stores nothing outside the device. Phase 2 will be self-hosted.
5. **Useful for anyone.** Goals, mileage rate, tax bracket, and state tax rate are all configurable — not hardcoded for one person.

---

## Out of Scope (Phase 1)

- GPS / automatic mileage tracking
- Bank / payment integration
- Push notifications
- Multi-device sync
- App Store distribution (PWA install replaces this)
- Progressive state tax bracket modeling (flat rate used as estimate)

---

## Success Metrics

- Route can be logged in under 30 seconds
- Quarterly tax estimate (federal + state) matches manual calculation within rounding
- App installs correctly as PWA on iOS and Android
- Coworkers can use it without instruction
- State tax rate can be changed in Settings and immediately reflects in the tax view

---

## Roadmap

| Phase | Scope | Hosting | Auth |
|---|---|---|---|
| 1.0 | Single user, core features | GitHub Pages | None |
| 1.1 | History, PDF export, state tax, swipe-delete | GitHub Pages | None |
| 1.2 | Onboarding, route editing, PWA, service worker | GitHub Pages | None |
| 2.0 | Multi-user, shared codebase | Self-hosted | Email or Google |
| 2.1 | PDF export v2, quarterly email reminders | Self-hosted | — |

---

*RouteLog is an independent project built by a Flex driver, for Flex drivers.*
