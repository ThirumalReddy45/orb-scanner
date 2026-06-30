# ORB Scanner — Deploy in 10 Minutes

## What you get
- FastAPI backend on Railway (free, always running)
- React PWA frontend on Vercel (free, permanent URL)
- Install on Android home screen — opens like a native app
- No code to run daily — just open and tap SCAN

---

## Step 1 — GitHub (2 min)

1. Go to https://github.com and create a free account if you don't have one
2. Click "New repository" → name it `orb-scanner` → Create
3. Upload the `backend/` folder files to the repo
4. Upload the `frontend/` folder files to the repo

Or use GitHub Desktop app — easier drag and drop.

---

## Step 2 — Deploy Backend on Railway (3 min)

1. Go to https://railway.app → Sign in with GitHub
2. Click "New Project" → "Deploy from GitHub repo"
3. Select your `orb-scanner` repo → select `backend` folder
4. Railway auto-detects Python → Click Deploy
5. Go to Settings → Variables → Add:
   ```
   KITE_API_KEY     = your_kite_api_key
   KITE_API_SECRET  = your_kite_api_secret
   ```
6. Go to Settings → Networking → Generate Domain
7. Copy your Railway URL — looks like:
   `https://orb-scanner-production.up.railway.app`

---

## Step 3 — Update Frontend with Railway URL (1 min)

Open these 2 files and replace `YOUR_RAILWAY_URL_HERE` with your actual Railway URL:

**frontend/.env.production**
```
VITE_API_URL=https://orb-scanner-production.up.railway.app
```

**frontend/vercel.json**
```json
"destination": "https://orb-scanner-production.up.railway.app/:path*"
```

Commit and push these changes to GitHub.

---

## Step 4 — Deploy Frontend on Vercel (2 min)

1. Go to https://vercel.com → Sign in with GitHub
2. Click "Add New Project" → Import your `orb-scanner` repo
3. Set Root Directory to `frontend`
4. Click Deploy
5. Vercel gives you a URL like:
   `https://orb-scanner.vercel.app`

---

## Step 5 — Install on Android as App (1 min)

1. Open Chrome on your Android phone
2. Go to your Vercel URL: `https://orb-scanner.vercel.app`
3. Tap the 3-dot menu (top right)
4. Tap "Add to Home screen"
5. Tap "Add"

Done. You now have ORB Scanner as an app icon on your home screen.

---

## Daily Usage

```
Tap ORB app icon on home screen
↓
Login with Kite (once per day)
↓
Wait until your ORB window closes (e.g. 9:45 AM for 30 min)
↓
Tap SCAN
↓
Signals appear with Entry, SL, Target, R:R
↓
Re-scan anytime during the day
```

---

## Kite API Setup (one time)

1. Go to https://developers.kite.trade
2. Login → Apps → Create new app
3. App name: ORB Scanner
4. Redirect URL: `https://YOUR_RAILWAY_URL.up.railway.app/callback`
5. Copy API Key and API Secret → paste in Railway environment variables

---

## Project Structure

```
orb-scanner/
├── backend/
│   ├── main.py           ← FastAPI + all scan logic
│   ├── requirements.txt
│   ├── railway.toml      ← Railway deployment config
│   └── Procfile
└── frontend/
    ├── src/
    │   ├── App.jsx       ← Full mobile-first React UI
    │   └── main.jsx
    ├── public/
    │   └── icons/        ← PWA app icons
    ├── index.html
    ├── package.json
    ├── vite.config.js    ← PWA plugin configured
    ├── vercel.json       ← Vercel + API proxy config
    └── .env.production   ← Set Railway URL here
```

---

## Tabs

**Tab 1 — ORB + Volume**
- Opening Range Breakout detection
- Volume confirmation (>1.5x by default, adjustable)
- Entry, Stop Loss, Target, R:R auto-calculated
- Resistance/Support level shown for each signal

**Tab 2 — Full Strategy**
- All Tab 1 filters plus:
- RSI > 60 (BUY) or < 40 (SELL)
- Price above/below Previous Day High/Low
- Nifty direction matches trade direction
- Only 3/5 or better signals shown

---

## Notes

- Backend stays always on with Railway (no sleep on paid plan; free plan sleeps after 30min — open the URL once to wake it)
- Scan anytime — app handles ORB window logic internally
- Change ORB window to 15, 30, 45 or any custom value anytime
- Stop scanning after 1:30 PM — low volume, choppy moves
