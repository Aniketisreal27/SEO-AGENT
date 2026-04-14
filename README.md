# Kalpi SEO Content Engine

Multi-agent SEO automation for Kalpi's investing content — built for Vercel.

## Deploy in 5 minutes

### 1. Get your Anthropic API key
Go to [console.anthropic.com](https://console.anthropic.com) → API Keys → Create key.

### 2. Push to GitHub
```bash
git init
git add .
git commit -m "Kalpi SEO Engine"
# create a repo on github.com, then:
git remote add origin https://github.com/YOUR_USERNAME/kalpi-seo-agent.git
git push -u origin main
```

### 3. Deploy on Vercel
1. Go to [vercel.com](https://vercel.com) → New Project
2. Import your GitHub repo
3. Click **Deploy** (Vercel auto-detects Vite — no config needed)

### 4. Add your API key
In Vercel → your project → **Settings** → **Environment Variables**:
```
Name:  ANTHROPIC_API_KEY
Value: sk-ant-xxxxxxxxxxxx
```
Click **Save**, then go to **Deployments** → **Redeploy**.

That's it. Your live URL is ready.

---

## Run locally

```bash
npm install
```

Create `.env`:
```
ANTHROPIC_API_KEY=sk-ant-xxxxxxxxxxxx
```

```bash
npm run dev
```

Open http://localhost:5173

---

## Architecture

```
Browser → /api/claude (Vercel Edge Function) → Anthropic API
                ↑
         API key lives only here — never in the browser
```

### Agents
| Agent | Role | Approach |
|-------|------|----------|
| SERP Intelligence | Analyses top 10 ranking pages | B |
| Content Brief | Structured brief before writing | A |
| Writer | Drafts full article to brief | Pipeline |
| Fact Checker | Validates Indian financial claims | Pipeline |
| SEO Scorer | Scores 0–100, title, slug | Pipeline |
| Cluster Planner | Pillar + 10 satellites | C |
| Refresh Monitor | Monthly SERP health check | B+C |

### Modes
- **Full pipeline** — SERP → Brief → Write → Fact-check → SEO score
- **Cluster planner** — Maps a complete topic cluster
- **Refresh monitor** — Assesses a published article's ranking health
