# Solo Planner

A planner for consultants and freelancers who work for several clients. In a single file, you plan your working days, log your time, track your contract days and follow the money you are still owed.

**In one sentence:** the independent consultant's pocket planner: days, hours and payments for every client in one place, with no accounts and no cloud.

## Highlights

- Works offline in the browser. No account, no server, no build step: it is one file, [index.html](index.html).
- Your data lives in a JSON file you own. Chrome and Edge save to it automatically; other browsers use Export / Import.
- Supports GBP, EUR and USD. Totals are per currency, with no conversion.
- Optional password lock and a "hide amounts" toggle for working in public.
- Light and dark themes (follows the system), print-friendly reports.

## Getting started

1. Open [index.html](index.html) in Chrome or Edge.
2. Set a password (it locks the page in this browser).
3. Create a new data file, or open an existing one. Put it in a folder synced by OneDrive, iCloud, Google Drive or Dropbox to get cloud backup for free.
4. Go to **Assignments** and add your first client engagement (or use "Load example data").

## The five tabs

### Assignments
One entry per client contract.

| Field | Meaning |
|---|---|
| Name | Client or assignment name |
| Color | Color used across all views (native color picker) |
| Billing | Day rate or hourly rate |
| Rate | Amount per day or per hour |
| Currency | GBP, EUR or USD |
| Start / End | Contract dates. End is optional (open-ended if empty) |
| Days I plan to work per week (Planner) | Default weekly plan. Feeds the Planner and the income forecast |
| Contract allowance | The days the client gave you. See "Contract allowance" below |
| Contract days | The number of days, when an allowance is chosen |
| Hours per day | Only for hourly billing. Converts hours to days (default 8) |
| Payment terms (days) | The due date is month end plus this number |

The tab also holds the data file controls (switch file, export a copy, import), the password settings, and "Clear all data".

### Planner
Planned days per week, one row per assignment.

- **Week view:** 14 weeks at a time. Capacity is 5 days a week. Weeks you leave alone follow the assignment's default. Change a cell to override it, or clear it to go back to the default. "Reset" restores the default for the 14 weeks shown.
- **Month view:** a read-only overview of planned days per month, worked out from the weekly plan, against the weekdays in each month. Select a month to open its weeks for editing.
- Totals row shows planned days and free days, and turns red when you are over capacity.

### Timesheet
Daily time logging.

- Week or month view, with previous / next navigation and a date picker.
- Enter days (0.5 steps, max 1 per day) for day-rate work, or hours (max 24) for hourly work.
- "Fill from plan" copies the planned days into empty cells.
- Each day can have a note. The notes for the period are listed below the table.
- Per-assignment and period totals, with the money value.
- **Days bank** below the table (see below).
- "Clear this week / month" deletes entries and notes for the period (with confirmation).

### Income
Money view, by month, per assignment.

Top tiles:

- **Received this year:** payments dated in the current year.
- **Outstanding:** logged work not yet marked received.
- **Overdue:** outstanding amounts past the payment terms.
- **Forecast, next 3 months:** work logged to date plus days planned after today.

Each month shows these columns per assignment:

| Column | Meaning |
|---|---|
| Logged | Time logged in the Timesheet, with its money value |
| Forecast | Logged to date plus planned days still to come in the month |
| Received | A **money amount** you type in, in the assignment's currency (£, € or $). The date field below it is the day the money arrived |
| Due | Month end plus payment terms |
| Status | In progress, Planned, Awaiting payment, Part received, Received, Overdue |

"Mark received" fills Received with the full logged amount. Assumptions: you invoice at month end; totals are per currency.

### Reports
Reports by week, month, quarter, half-year or year, for all assignments or one.

- Tiles: days worked, utilisation (against Mon-Fri working days), earned, received.
- Tables: by assignment, by day / week / month, and a detail list with notes.
- **Export:** CSV download, or Print / save as PDF.

## Contract allowance (the Days bank)

The allowance tracks how many days the client contracted, so you can see how many are left. It is separate from the planned days.

| | Planned days per week | Contract allowance |
|---|---|---|
| What it is | Your intention: days you plan to work | The contract limit: days the client gave you |
| Feeds | Planner and income forecast | Days bank in the Timesheet |
| Can change | Week by week in the Planner | Fixed per assignment |

Options:

- **None:** no tracking (default).
- **Per week, unused roll over:** X days per week. Unused days carry to the next week with no expiry.
- **Per month, unused roll over:** X days per month, same rollover.
- **One total pot of days:** one total for the whole contract; every worked day is subtracted.

The Days bank table in the Timesheet shows, per assignment:

- **Carried in:** what is left from earlier periods (shown as "—" for a total pot).
- **Allowance:** new days for this period.
- **Used:** days logged. Hourly work is converted using Hours per day.
- **Days left:** Carried in + Allowance - Used. A negative number (shown in red) means you used more than the contract.

Allowance only accrues for periods that overlap the assignment's start and end dates.

**Example: two weeks at 3 days per week.** Set Start to the Monday of week 1, End to the last day of week 2, Days I plan to work per week to 3, Contract allowance to *Per week, unused roll over* with 3 contract days. If you use 2 days in week 1, week 2 shows 1 carried in + 3 = 4 available. (Alternative: a total pot of 6.) Days always roll over; there is no option for days that expire at the end of the week.

When you choose "Per week" and the Contract days field is empty, it is pre-filled with the planned days per week.

## Data and privacy

- **Storage:** one JSON file. It holds assignments, the weekly plan, time entries, payments and notes.
- **Saving:** automatic in Chrome / Edge (File System Access API), about 0.6 s after a change. Status is shown at the top right.
- **Conflicts:** if the file changes elsewhere (another device or sync service), a banner lets you load the file's version or overwrite it with yours.
- **Other browsers:** memory only. Use Export copy in the Assignments tab.
- **Password lock:** a screen lock for this browser only. The password is hashed (PBKDF2, 200,000 iterations) in local storage. It does **not** encrypt the data file.
- **Hide amounts:** masks money values on screen. Resets to hidden each session.
- **Network:** the only external request is Google Fonts (IBM Plex). Everything else is local.

## Tech notes

- Single file with inline CSS and JavaScript, no dependencies or build step.
- Fonts: IBM Plex Sans and IBM Plex Mono.
- Data keys: entries `assignmentId|YYYY-MM-DD`, plan `assignmentId|week-Monday`, payments `assignmentId|YYYY-MM`.
- Colors are stored per assignment in the data file. The default palette in `COLORS` is used only to pre-select a color for a new assignment.
