# To Do — A little progress every day.

A minimal personal daily checklist for one person. React + TypeScript, no backend, no accounts.
Everything is saved in the browser's LocalStorage on the device.

## Put it on the iPad

The app is a folder of static files (`dist/`). It must be served over **HTTPS** so the iPad can install it.
Any static host works; the easiest options:

- **Netlify Drop** — go to app.netlify.com/drop and drag the `dist` folder in. You get an https link.
- **GitHub Pages / Cloudflare Pages / Vercel** — publish the contents of `dist`.

Then on the iPad, open the link in **Safari → Share → Add to Home Screen**. It opens full-screen like an app and works offline.

### Important: where your data lives

- Data is stored **on that device, inside that browser/app** — nothing is uploaded.
- On iPad, the **Home Screen app and Safari have separate storage**. Pick one (the Home Screen app is recommended) and use it consistently.
- Installing to the Home Screen also protects the data from Safari's automatic clean-up of unused websites.
- Use **Settings → Export backup** now and then. **Import backup** restores it (also the way to move data between devices).

## How it works

- **Days** use the Africa/Cairo calendar, whatever the device's own timezone is. A new day starts with an empty list; nothing carries over.
- **Active day** = at least one task completed. **Perfect day** = at least one task and all of them completed.
  The two streaks are calculated separately from the saved daily records. Today is never counted as a failure
  until it is over, and a perfect today counts immediately.
- **Averages** use only days that have tasks. Days without tasks are not counted as 0%.
- **Past days are read-only** in History, so a finished day's record can't be changed by accident. You can delete a whole day (with confirmation).
- Every change is written to LocalStorage immediately. Importing or deleting everything keeps a safety copy of the previous data under the key `todo:data:before-import`.
  Unreadable saved data is copied aside (`todo:data:corrupt:<time>`) instead of being overwritten.

## Develop

```bash
npm install
npm run dev        # http://localhost:5173 with live rebuild
npm run build      # production build into dist/
npm test           # logic tests (dates, streaks, model, validation)
npm run test:e2e   # real-browser test at iPad sizes (needs Playwright + Chrome; set CHROME_PATH if needed)
npm run typecheck
```

Source layout: `src/lib` (dates, model, stats, storage, backup — no React), `src/pages` (Today, Dashboard, History),
`src/components`, `src/hooks.ts`, `src/styles.css`. Icons are regenerated with `npm run icons`.
