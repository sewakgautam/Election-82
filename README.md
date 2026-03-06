# 🇳🇵 Nepal Election Dashboard 2082

Live election results dashboard for Nepal's House of Representatives election 2082 (2026).
Data is scraped directly from the **Election Commission of Nepal** (`result.election.gov.np`) — no manual updates needed.

## Features
- ✅ Live data from ECN — auto-refreshes every 60 seconds
- ✅ Party-wise seat totals (FPTP + PR = Total)
- ✅ Parliament bar visualization with majority marker
- ✅ All parties ranked by total seats
- ✅ Server-side scraping via Next.js API route (no CORS issues)
- ✅ Vercel-ready — one-click deploy

## Deploy to Vercel

### Option 1: GitHub + Vercel (recommended)
1. Push this folder to a GitHub repo
2. Go to [vercel.com](https://vercel.com) → New Project → Import your repo
3. Vercel auto-detects Next.js — just click **Deploy**
4. Done! Your dashboard is live and updates itself.

### Option 2: Vercel CLI
```bash
npm install -g vercel
cd nepal-election
npm install
vercel
```

## Local Development
```bash
npm install
npm run dev
# Open http://localhost:3000
```

## How it works

```
Browser → /api/results (Next.js API route on Vercel)
                ↓
         Scrapes result.election.gov.np
                ↓
         Parses HTML for party seat data
                ↓
         Returns JSON → Dashboard renders
```

The API route at `pages/api/results.js` runs server-side on Vercel, bypassing CORS restrictions. It's cached for 60 seconds (`Cache-Control: s-maxage=60`) so rapid page loads don't hammer ECN.

## Structure
```
nepal-election/
├── pages/
│   ├── index.js          # Main dashboard UI
│   └── api/
│       └── results.js    # Server-side scraper API
├── lib/
│   └── scraper.js        # ECN scraping + parsing logic
├── styles/
│   └── globals.css       # Dark theme styles
└── vercel.json           # Vercel config
```

## Notes
- The ECN site (`result.election.gov.np`) renders dynamically — we parse its HTML tables
- If ECN changes their HTML structure, update `lib/scraper.js` accordingly
- PR seat data comes from `result.election.gov.np/PRVoteChartResult2082.aspx`
- Counting for FPTP starts within 24h of polls closing; PR takes 3-5 days
