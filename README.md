# Princess Hair Luxe — Deployment Guide

This is a ready-to-deploy version of your site, built with Vite + React + Tailwind.

## ⚠️ Read this first: the admin data limitation

Inside Claude, the admin panel (products, orders, discount codes) used Claude's
shared cloud storage. That only works inside Claude artifacts.

This version replaces it with **your browser's localStorage** (see
`src/storage.js`) so the site still runs standalone. That means:

- Data is saved **per browser, per device** — not a real shared database.
- An order placed by a customer on their phone will **not** appear in your
  admin panel on your laptop.
- Discount codes generated on one device can't be redeemed from another.
- Clearing your browser's site data wipes everything.

This is fine to launch with and test, but for real multi-device order
management you'll eventually want a proper backend (Firebase, Supabase, or a
small custom API). The rest of the app won't need to change — only
`src/storage.js` would be swapped out. Ask Claude for help with that when
you're ready.

## 1. Create a GitHub repository

1. Go to [github.com/new](https://github.com/new)
2. Name it whatever you like — you don't need to match anything in the code, name it here
3. Create the repository (public, no README/gitignore needed — you already have them)

## 2. Push this code to GitHub

From this project folder, run:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git
git push -u origin main
```

## 3. Install dependencies and deploy

```bash
npm install
npm run deploy
```

This builds the site and pushes it to a `gh-pages` branch automatically
(via the `gh-pages` package already included in `package.json`).

## 4. Turn on GitHub Pages

1. On GitHub, go to your repo → **Settings** → **Pages**
2. Under "Build and deployment", set **Source** to "Deploy from a branch"
3. Set **Branch** to `gh-pages` / `root`, then Save

Within a minute or two, your site will be live at:

```
https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/
```

## Local testing before you deploy

```bash
npm install
npm run dev
```

Then open the local URL it prints (usually `http://localhost:5173`).

## Updating the site later

Whenever you make changes:

```bash
git add .
git commit -m "Describe your change"
git push
npm run deploy
```

## Custom domain — removed for now

This version does **not** use a custom domain — it's set up to serve from
the plain GitHub Pages URL (`https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/`),
since that's the simplest, most reliable setup and avoids DNS-related 404s.

**If you previously entered a custom domain in GitHub**, clear it too:

1. Repo → **Settings** → **Pages**
2. Under "Custom domain", delete whatever's in that field → Save
3. Redeploy: `npm run deploy`

Your site will then be reachable at:
```
https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/
```

If you want to add `princesshairluxe.com` back later, that's straightforward
to re-enable — just ask.
