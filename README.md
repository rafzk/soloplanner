# Solo Planner

A planner for consultants and freelancers who work for several clients. In a single file, you plan your working days, log your time, track your contract days and follow the money you are still owed.

**In one sentence:** the independent consultant's pocket planner: days, hours and payments for every client in one place, with no accounts and no cloud.

## Highlights

- Works offline in the browser. No account, no server, no build step: it is one file, [index.html](index.html).
- Your data lives in a JSON file you own. Chrome and Edge save to it automatically; other browsers use Export / Import.
- Supports GBP, EUR and USD. Totals are per currency, with no conversion.
- Optional password lock and a "hide amounts" toggle (remembered in the browser).
- Undo for destructive actions, keyboard navigation in grids, light and dark themes, print-friendly reports.

## Getting started

1. Open [index.html](index.html) in Chrome or Edge.
2. Create a new data file, or open an existing one. Put it in a folder synced by OneDrive, iCloud, Google Drive or Dropbox for free cloud backup.
3. Add your first client (or use "Load example data").
4. A short "Getting started" checklist on the Today tab tracks the first steps. Dismiss it any time.

A password is optional: set it later in Clients › Password.

## The six tabs

### Today
The daily view, with big targets that also work on a phone.

- One card per client running today: **− / +** buttons (0.5 day or 1 hour), **Half day / Full day** quick buttons, and a note box.
- Shows planned days for today and the contract days left.
- A "This week" strip: tap a day to cycle full day, half day, none (day-rate clients) or type hours (hourly clients). "Fill week from plan" copies the plan.

### Planner
Planned days per week, one row per client.

- **Week view:** 14 weeks at a time. Weeks you leave alone follow the client's default. Change a cell to override it, or clear it to go back to the default. "Reset row" restores the default for the weeks shown (with undo). A legend explains the shading.
- **Month view:** a read-only overview per month against capacity. Select a month, or use "Open weeks", to edit its weeks.
- **Capacity** is your working days per week (default 5; set it in Clients › Settings).

### Timesheet
Daily time logging for the week or the month.

- Enter days (0.5 steps, max 1 per day) for day-rate work, or hours (max 24) for hourly work.
- Arrow keys and Enter move between cells. × clears an entry (with undo). ✎ adds a note.
- "Fill from plan" copies the planned days into empty cells (with undo).
- Weekends can be hidden (days with entries stay visible).
- **Contract days left** table below the grid (see below).

### Income
Money view, by month, per client.

Top tiles: Received this year, Outstanding, Overdue, Forecast for the next 3 months.

| Column | Meaning |
|---|---|
| Logged | Time logged in the Timesheet, with its money value |
| Forecast | Logged to date plus planned days still to come in the month |
| Invoice | Optional invoice number and the date you sent it |
| Received | A **money amount** you type in, in the client's currency (£, € or $), plus the date it arrived. "Mark received" fills the full logged amount |
| Due | Invoice sent date (or month end if none) plus payment terms, with year |
| Status | In progress, Planned, Invoiced, Awaiting payment, Part received, Received, Overdue |

Earlier months are collapsed under "Earlier months".

### Reports
Reports by week, month, quarter, half-year or year, for all clients or one.

- Tiles: days worked, utilisation (with a progress bar), earned, received.
- A stacked column chart of days worked per period, in each client's colour. The tables below carry the exact numbers.
- Tables: by client, by day / week / month, and a detail list with notes.
- **Export:** CSV download, or Print / save as PDF.

### Clients
Client list first; "Add client" opens the form.

| Group | Fields |
|---|---|
| Client | Name, Color |
| Billing | Day or hourly rate, Rate, Currency, Hours per day (hourly only) |
| Dates and payment | Start, End (optional), Payment terms (days) |
| Days | Days I plan to work per week, Contract allowance, Contract days |

Each field shows inline help, and errors appear next to the field. Below the list:

- **Settings:** working days per week (capacity), date and number format (UK, US, Portuguese, Spanish, French, German), hide weekends. Weeks always start on Monday.
- **Data file:** switch file, export a copy, import.
- **Password (optional):** set, change, lock now, remove.

## Plan vs contract days

Two separate ideas:

| | Days I plan to work per week | Contract allowance |
|---|---|---|
| What it is | Your intention | The days the client contracted |
| Feeds | Planner and income forecast | "Contract days left" in the Timesheet |
| Can change | Week by week in the Planner | Fixed per client |

Contract allowance options: **None**, **Per week** (unused roll over), **Per month** (unused roll over), **One total pot of days**.

The "Contract days left" table shows, per client: **Carried in**, **New days**, **Logged**, **Days left**. A negative number (red) means you logged more than the contract allows. Unused days always roll over, with no expiry. Days only accrue for periods that overlap the client's start and end dates. Hourly work is converted using Hours per day.

**Example: two weeks at 3 days per week.** Start = Monday of week 1, End = last day of week 2, plan 3 days per week, allowance *Per week* with 3 contract days. If you log 2 days in week 1, week 2 shows 1 carried in + 3 = 4 available. (Alternative: a total pot of 6.)

## Data and privacy

- **Storage:** one JSON file with clients, plan, time entries, notes, invoices, payments and settings.
- **Saving:** automatic in Chrome / Edge (File System Access API), about 0.6 s after a change. A status pill at the top right shows the state; save errors and file conflicts also show a banner with actions.
- **Other browsers:** changes are only in memory. A banner offers "Export a copy now".
- **Undo:** clearing an entry, resetting a row, filling from plan, marking received, deleting a client, clearing a week or all data, and replacing data from an import can be undone from the toast for a few seconds.
- **Password lock:** optional screen lock for this browser only. The password is hashed (PBKDF2, 200,000 iterations) in local storage. It does **not** encrypt the data file.
- **Hide amounts:** masks money values on screen. Visible by default; the choice is remembered.
- **Network:** the only external request is Google Fonts (IBM Plex). Everything else is local.

## Tech notes

- Single file with inline CSS and JavaScript, no dependencies or build step.
- Data keys: entries `clientId|YYYY-MM-DD`, plan `clientId|week-Monday`, payments and invoices `clientId|YYYY-MM`. The data file still calls clients `assignments`.
- Colors are stored per client. The default palette in `COLORS` only pre-selects a color for a new client.
