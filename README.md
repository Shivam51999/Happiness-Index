# Mangalam Happiness Tracker

Static pages for tracking employee happiness & satisfaction at Mangalam Landmarks.

## Pages
- `index.html` — landing page with links to all tools
- `self-report.html` — monthly self-report form (employees) — **identity comes from `?id=` in the URL, no name dropdown**
- `manager-input.html` — monthly manager perception form (managers) — **identity comes from `?manager=` in the URL; team list is filtered to that manager's direct reports only**
- `dashboard.html` — HR/CEO dashboard (currently running on demo data)
- `generate-links.html` — admin tool: pulls the live roster and produces each person's unique link for the month

## How identity works (read this before sharing links)
Earlier versions of these forms let anyone pick any name from a dropdown — which meant someone could submit as a colleague, or a manager, or even rate themselves. That's fixed by removing the dropdown entirely:

- Each employee's self-report link looks like `self-report.html?id=EMP_0042`. The `id` must match a `Roster` row exactly, and the form shows that person's name as a fixed label — not editable.
- Each manager's link looks like `manager-input.html?manager=Ram%20Phuge`. The team dropdown only shows people whose `Manager` column in the roster matches that exact name.
- Use `generate-links.html` every month to produce the current list of links from the live roster, then send each link privately (WhatsApp DM / personal email) — never post them in a shared group, since anyone with the link can submit under that identity.

**Limitation to know about:** this stops casual misuse (picking a name from a list) but doesn't stop someone who deliberately edits the URL parameter by hand. For a small trusted internal team this is usually an acceptable tradeoff against the cost of building real authentication — but it's not a hard security boundary.

## Before going live
Open `self-report.html`, `manager-input.html`, `dashboard.html`, and `generate-links.html` and replace:
```js
var APPS_SCRIPT_URL = 'PASTE_YOUR_WEB_APP_URL_HERE';
```
with your deployed Apps Script Web App URL in all four files.

In `generate-links.html`, also set the "GitHub Pages base URL" field to wherever this repo ends up living (e.g. `https://your-username.github.io/mangalam-happiness/`).

In `dashboard.html`, replace `DEMO_DATA` with a live fetch to `?action=dashboard&month=YYYY-MM`.

## Hosting
Served via GitHub Pages from the `main` branch, root folder.

