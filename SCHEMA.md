# RouteLog — Canonical Data Schema
**Version:** 1.0  
**Status:** Active  
**Last Updated:** 2026-04-16

This document defines the authoritative data structures for RouteLog. All frontend localStorage keys and future backend database tables must conform to these schemas. Any changes to field names, types, or structure must be versioned here first.

---

## Route Object

A route is the core data unit — a single delivery block pairing earnings and mileage as one record.

```json
{
  "id": 1713276000000,
  "date": "2026-04-16",
  "earnings": 87.50,
  "miles": 42.3,
  "startTime": "09:00",
  "endTime": "12:30",
  "type": "Flex",
  "notes": "Heavy traffic on M-59, good tips"
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | integer | yes | Unix timestamp in ms at time of creation. Used as unique key. |
| `date` | string | yes | ISO 8601 date: `YYYY-MM-DD`. The calendar date the route was worked. |
| `earnings` | float | yes | Total gross pay for the block in USD. Must be > 0. |
| `miles` | float | no | Miles driven for this block. Defaults to 0 if not entered. |
| `startTime` | string | no | Block start time in `HH:MM` (24-hour). Used to calculate duration and hourly rate. |
| `endTime` | string | no | Block end time in `HH:MM` (24-hour). |
| `type` | string | yes | Route platform/type label. One of the user-configured route types. Defaults to `"Flex"`. |
| `notes` | string | no | Free-text notes. Max 500 characters recommended. |

**Derived fields** (computed at render time, never stored):
- `duration_hours` = `(endTime - startTime)` in decimal hours
- `hourly_rate` = `earnings / duration_hours`
- `mileage_deduction` = `miles × (mileageRate / 100)`

---

## Settings Object

Stored as a single JSON blob. All fields have defaults and are user-overridable.

```json
{
  "weeklyGoal": 800,
  "monthlyGoal": 3200,
  "mileageRate": 70,
  "fedBracket": 22,
  "stateRate": 4.25,
  "routeTypes": ["Flex", "DSP", "DoorDash", "Instacart", "Other"]
}
```

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `weeklyGoal` | float | `800` | Target weekly earnings in USD. |
| `monthlyGoal` | float | `3200` | Target monthly earnings in USD. |
| `mileageRate` | float | `70` | IRS standard mileage rate in **cents** per mile. 2025 rate: 70¢. |
| `fedBracket` | float | `22` | Federal marginal income tax bracket as a percentage (e.g. `22` = 22%). |
| `stateRate` | float | `4.25` | State income tax rate as a percentage. Michigan default: 4.25%. |
| `routeTypes` | array of strings | see above | User-configurable list of route type labels. At least one must exist. |

---

## localStorage Keys (Phase 1)

| Key | Value | Description |
|-----|-------|-------------|
| `rl_routes` | JSON array of Route objects | All logged routes, unsorted. |
| `rl_settings` | JSON Settings object | User preferences. Merged with DEFAULTS on read. |
| `rl_onboarded` | `"1"` | Set after user completes or skips onboarding. |

---

## IRS Quarter Definitions

Used by the Tax View. These are the **IRS-defined** earnings periods and payment due dates.

| Quarter | Earnings Period | Payment Due Date |
|---------|----------------|-----------------|
| Q1 | Jan 1 – Mar 31 | April 15 |
| Q2 | Apr 1 – May 31 | June 15 |
| Q3 | Jun 1 – Aug 31 | September 15 |
| Q4 | Sep 1 – Dec 31 | January 15 (following year) |

> **Note:** Q2 and Q3 are intentionally asymmetric. Q2 is only 2 months (April–May). Q3 is 3 months (June–August). This matches IRS Form 1040-ES instructions exactly.

---

## Tax Calculation Logic

Applied per quarter using the user's settings.

```
mileage_deduction   = miles × (mileageRate / 100)
net_for_se          = max(0, earnings − mileage_deduction)
se_tax              = net_for_se × 0.9235 × 0.153
se_deduction        = se_tax / 2
net_taxable         = max(0, net_for_se − se_deduction)
fed_income_tax      = net_taxable × (fedBracket / 100)
state_income_tax    = net_taxable × (stateRate / 100)
total_due           = se_tax + fed_income_tax + state_income_tax
```

> This is an **estimate** for planning purposes, not tax advice. Displayed disclaimer required in all tax views and PDF exports.

---

## Phase 2 — Backend Schema (Planned)

When the backend is added, routes and settings will move from localStorage to a PostgreSQL database. The field names and types above map directly to database columns. The `id` field will transition from a client-generated timestamp to a server-generated UUID or auto-increment integer.

### Planned Tables

**users**
| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID | Primary key |
| `google_id` | string | From Google OAuth |
| `email` | string | From Google OAuth |
| `display_name` | string | From Google OAuth |
| `created_at` | timestamp | |

**routes**
| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID | Primary key |
| `user_id` | UUID | Foreign key → users.id |
| `date` | date | `YYYY-MM-DD` |
| `earnings` | decimal(8,2) | |
| `miles` | decimal(7,1) | Nullable |
| `start_time` | time | Nullable |
| `end_time` | time | Nullable |
| `type` | string | |
| `notes` | text | Nullable |
| `created_at` | timestamp | |
| `updated_at` | timestamp | |

**settings**
| Column | Type | Notes |
|--------|------|-------|
| `user_id` | UUID | Primary key (one row per user) |
| `weekly_goal` | decimal(8,2) | |
| `monthly_goal` | decimal(8,2) | |
| `mileage_rate` | decimal(4,2) | In cents |
| `fed_bracket` | decimal(4,2) | Percentage |
| `state_rate` | decimal(4,2) | Percentage |
| `route_types` | JSON array | |
| `updated_at` | timestamp | |
