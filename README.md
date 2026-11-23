# Steady

A calm, private tracker for the things that are easy to lose track of when life is heavy:
**deadlines, recurring payments, contracts (with cancel-by dates), and a simple monthly budget.**

- **Private by design.** No account, no server, no tracking. Data lives in your browser's storage and never leaves your device unless you export it.
- **Contracts that don't trap you.** Enter the term end, notice period and renewal rhythm. Steady works out the last day to cancel, what happens if you've already missed it, and roughly what waiting costs. After you cancel, it reminds you to get written confirmation.
- **Real reminders.** Export a `.ics` file (More → Download calendar file) and your phone's calendar does the alerting: a week before, two days before, and on the day.
- **Gentle on purpose.** "Just one thing" mode. No red alarms or guilt copy. Undo on every action.
- **Works offline** and installs to the home screen (PWA).

## Run locally

```sh
npm run dev      # serves on http://localhost:8123 (needs python3), or use any static server
npm test         # logic tests (node:test, no dependencies)
```

## Deploy on Vercel

It's a plain static site: no build step, no dependencies.

1. Push this folder to a GitHub repo.
2. In Vercel: **Add New → Project →** import the repo. Framework preset: **Other**. Leave build command and output directory empty.
3. Deploy. `vercel.json` adds a strict Content-Security-Policy and security headers.

(Or from this folder: `npx vercel --prod`.)

## Files

| File | What it is |
|---|---|
| `js/logic.js` | All the rules: dates, notice periods, budget maths, calendar export, input cleaning. Pure functions, fully tested. |
| `js/store.js` | Browser storage, backup/restore. |
| `js/app.js` | The interface. |
| `tests/logic.test.mjs` | Tests, including "notice date already missed" and month-end edge cases. |
| `sw.js`, `manifest.webmanifest` | Offline + install to home screen. |

## Known limits (honest list)

- Data is per browser/device. Moving device = export a backup, then restore it there.
- No push notifications (a static site can't send them). The calendar export is the reminder mechanism.
- English only for now; amounts accept both `12,50` and `12.50`.
- The cancel-by logic follows what you enter. It doesn't know the law or your contract. Check the actual terms.
