# StarJar

A reward chart for kids and tweens: chores earn stars, and stars redeem
parent-approved rewards. No account, no server.

Formerly Mission Stars / Kids Reward Chart — renamed StarJar on Nov 2, 2026.

Live shareable version (Muse-hosted): see the link in the chat where this
was built. The code in this repo is the same app as a single static file.

## What it does

- Kid profiles: **none pre-loaded** — the chart starts empty, add your
  own profiles in Parent controls (name, emoji, favourite colour)
- Chores worth stars, with 12 default chores pre-loaded
  - Assign a chore to Everyone, one kid, or any combination of kids
  - Daily (resets each morning), Weekly (resets on Mondays), or Anytime
  - A daily/weekly chore can't be earned twice until it resets
- Rewards shop, with 9 reward ideas pre-loaded in the shared list
  - Assign a reward to specific profiles when adding/editing it
  - Pre-approved rewards redeem instantly ("Get it now!")
  - Other rewards go to "Waiting for a parent" — stars are spent only
    when a parent taps Yes; declining keeps the stars
- Parent mode, protected by an optional 4–6 digit PIN (on-screen keypad)
- Bonus stars and penalties, both ways:
  - Ad-hoc, with a custom star amount and reason
  - Reusable parent-set rules, one tap to apply (6 bonus rules and
    5 penalty rules pre-loaded; add, edit, and delete your own)
  - Balances never go below zero
- History tab: every star earned, bonus, penalty, and redemption,
  with Undo. History keeps the latest 200 entries; balances stay.

## Data and offline use

All data is saved **on the device itself, in the browser's localStorage**
(key `kids-reward-chart-shareable-v1` in this export — kept unchanged
so renaming the app does not erase existing stars). There is no server,
no account, and no sync.

- Losing internet does **not** erase data. Once the page has loaded,
  the chart, stars, chores, and history are already on the device.
- You do need internet the first time you open the link, to load the
  page (and the Google Fonts it uses — it falls back to system fonts
  offline).
- Data is per device and per browser: the Kindle and the iPad each keep
  their own chart. Stars earned on one do not appear on the other.
- Data *is* lost if you clear that browser's site data, use private /
  incognito mode, or uninstall / reset the browser. Don't clear site
  data for this page if you want to keep the stars.
- Safari: if the app is only opened in a Safari tab (not Add to Home
  Screen), Safari can delete script-written storage after 7 days of
  Safari use with no interaction on the site. Home-screen web apps are
  exempt — install it to the Home Screen.

## Run locally (dev / testing)

No build step, no dependencies, no install. Any static file server works.

### Option 1 — open the file directly

Double-click `index.html`, or open it in a browser from the file menu.
This works for a quick look, but some browsers restrict local files —
use Option 2 for reliable testing.

### Option 2 — local server (recommended)

```bash
cd starjar
python3 -m http.server 8000
# then open http://localhost:8000 in your browser
```

Or with Node:

```bash
npx serve .
# then open the URL it prints
```

### Option 3 — VS Code

Install the "Live Server" extension, right-click `index.html` →
"Open with Live Server".

## Test checklist

1. Open the app — it should start with no kid profiles. Add one in
   Parent controls.
2. Complete a daily chore — balance goes up, chore shows Done.
   Try it again the same day — it should be blocked until reset.
3. In Parent mode, give an ad-hoc bonus (+3, with a reason) and an
   ad-hoc penalty (−2, with a reason). Balance must never go below 0.
4. Apply a bonus rule and a penalty rule with one tap.
5. Redeem a pre-approved reward — stars deduct instantly.
   Request a non-approved reward — it waits for a parent, stars
   deduct only on Yes.
6. Assign a reward to a specific profile and check it shows for them.
7. Reload the page — balances, chores, and History must still be there.
8. Turn off Wi-Fi and reload the page from the browser cache / home
   screen icon — data must still be there. (First load needs internet.)

## Kindle Fire / iPad install

1. Open the shareable link in Silk (Kindle) or Safari (iPad).
2. Kindle: three-dot menu → Add to Home Screen.
   iPad: Share icon → Add to Home Screen.
3. Name it **StarJar** and tap Add.
4. Open it from the Home Screen icon. Add kid profiles and set the
   parent PIN on each device — those settings are per device.

## Files

- `index.html` — the whole app: HTML, CSS, and JavaScript in one file.
- `README.md` — this file.

## Enhancing it

The app is intentionally one file so it's easy to change. To add a
feature, edit `index.html` directly and reload — no build step.

Ideas that fit the current design: weekly star goals, streaks, a
parent dashboard / weekly summary, exporting History, or per-kid
reward lists. Keep new parent-only actions behind the PIN check in
Parent mode, and keep balances from going below zero.
