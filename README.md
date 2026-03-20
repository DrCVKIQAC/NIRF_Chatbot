# NIRF Assist 2025 — Deployment Guide
## Dr C V Krishnaveni · SKR & SKR GCW(A), Kadapa
## Zero cost · 15 minutes · Free forever

---

## What you will set up

```
Anyone in India
      ↓  opens URL (no login, no app, no key)
GitHub Pages  ──  serves index.html (FREE, always-on)
      ↓  sends question
Cloudflare Worker  ──  adds secret API key (FREE, always-on)
      ↓  calls AI
Gemini 1.5 Flash  ──  answers (FREE, 1M tokens/day)
```

**Total cost: ₹0. Forever.**

---

## STEP 1 — Get your free Gemini API key (3 minutes)

1. Open: https://aistudio.google.com/app/apikey
2. Sign in with any Gmail account
3. Click **"Create API Key"**
4. Copy the key (looks like: `AIzaSyA...`)
5. Save it safely — you will need it in Step 3

---

## STEP 2 — Deploy the Cloudflare Worker (8 minutes)

This hides your API key. Users never see it.

1. Go to: https://dash.cloudflare.com
2. Sign up free (no credit card needed)
3. Click **"Workers & Pages"** in the left menu
4. Click **"Create"** → **"Create Worker"**
5. Delete all the default code in the editor
6. Open `worker.js` from this folder and **paste the entire contents**
7. Click **"Save and Deploy"**
8. You will see a URL like:
   ```
   https://nirf-proxy.yourname.workers.dev
   ```
   **Copy this URL — you need it in Step 4**

9. Click **"Settings"** tab → **"Variables"**
10. Click **"Add variable"**:
    - Variable name: `GEMINI_API_KEY`
    - Value: paste your key from Step 1
    - ✅ **Tick "Encrypt"** (hides it from everyone including you)
11. Click **"Save and Deploy"**

✅ Your Worker is live. The API key is safe and hidden.

---

## STEP 3 — Edit index.html (1 minute)

1. Open `index.html` in any text editor (Notepad, VS Code, etc.)
2. Find this line near the top of the `<script>` section:
   ```javascript
   const WORKER_URL = 'https://YOUR-WORKER.YOUR-SUBDOMAIN.workers.dev';
   ```
3. Replace the placeholder URL with your actual Worker URL from Step 2:
   ```javascript
   const WORKER_URL = 'https://nirf-proxy.yourname.workers.dev';
   ```
4. Save the file

---

## STEP 4 — Publish on GitHub Pages (4 minutes)

1. Go to: https://github.com
2. Sign up free if you don't have an account
3. Click **"+"** → **"New repository"**
4. Name it: `nirf-assist` (or any name you like)
5. Set to **Public**
6. Click **"Create repository"**
7. Click **"uploading an existing file"**
8. Drag and drop `index.html` into the upload box
9. Click **"Commit changes"**
10. Go to **Settings** → **Pages** (left sidebar)
11. Under "Source", select **"Deploy from a branch"**
12. Branch: **main**, Folder: **/ (root)**
13. Click **Save**
14. Wait 1–2 minutes
15. Your site is live at:
    ```
    https://YOUR-GITHUB-USERNAME.github.io/nirf-assist/
    ```

✅ Share this URL with any college in India. Works immediately.

---

## Your final URLs

| What | URL |
|------|-----|
| **Chatbot (share this)** | `https://YOUR-USERNAME.github.io/nirf-assist/` |
| Cloudflare Worker | `https://nirf-proxy.YOUR-NAME.workers.dev` |
| Gemini API Console | https://aistudio.google.com/app/apikey |
| GitHub repo | `https://github.com/YOUR-USERNAME/nirf-assist` |

---

## Free tier limits — will it run out?

| Service | Free limit | Your usage | Safe? |
|---------|-----------|------------|-------|
| GitHub Pages | 100GB/month bandwidth | ~50KB × visits | 2 million visits/month before limit |
| Cloudflare Worker | 100,000 requests/day | ~2 per chat message | 50,000 conversations/day |
| Gemini 1.5 Flash | 1,500 requests/day, 1M tokens/day | ~1 request per message | 1,500 messages/day |

**For college use across Andhra Pradesh, you will never hit these limits.**

---

## Updating the chatbot

To update the chatbot (new features, new data):
1. Edit `index.html` on your computer
2. Go to your GitHub repo
3. Click `index.html` → Click the pencil ✏️ edit icon
4. Paste the new content
5. Click **"Commit changes"**
6. Live in 1–2 minutes

---

## Custom domain (optional, still free)

If your college has a domain (e.g. `skrgcw.ac.in`):
1. GitHub Pages → Custom domain → enter your domain
2. Add a CNAME record in your DNS pointing to `YOUR-USERNAME.github.io`
3. GitHub provides free SSL automatically

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| "Could not reach AI server" | Check WORKER_URL in index.html matches your Worker URL exactly |
| Worker returns 500 error | Check GEMINI_API_KEY is set in Worker Settings → Variables |
| GitHub page shows 404 | Wait 2 minutes after enabling Pages; check branch is "main" |
| Gemini rate limit error | Free tier = 15 req/min. Wait a moment and retry |
| CORS error in browser console | Re-deploy worker.js — it has the CORS headers built in |

---

## Support

Developed by **Dr C V Krishnaveni**
Department of Computer Science
SKR & SKR Government College for Women (Autonomous)
Kadapa, Andhra Pradesh, India

License: CC BY-NC 4.0 (content) + MIT (code) | Zero Cost Forever
