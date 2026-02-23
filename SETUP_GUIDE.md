# TaskPilot — Complete Setup Guide

## Your 5 Files

| File | What it does |
|---|---|
| `index.html` | The entire app — all screens, logic, UI |
| `manifest.json` | Tells iOS/Android it's an installable app |
| `sw.js` | Service worker — makes it work offline |
| `icon-192.png` | App icon (home screen, small) |
| `icon-512.png` | App icon (home screen, large) |

All 5 files must be in the **same folder** when you upload them.

---

## PART 1 — Host the App on GitHub Pages (Free, 10 min)

> You need to host the files online so Safari can add them to your iPhone home screen. GitHub Pages is free and takes about 10 minutes.

### Step 1 — Create a GitHub account
1. Go to **github.com**
2. Click **Sign up**
3. Follow the steps (free account is fine)

### Step 2 — Create a new repository
1. Once logged in, click the **+** icon (top right) → **New repository**
2. Repository name: `taskpilot` (lowercase, no spaces)
3. Make sure it's set to **Public**
4. Do NOT tick "Add a README file"
5. Click **Create repository**

### Step 3 — Upload your 5 files
1. On the repository page, click **uploading an existing file** (you'll see this link in the middle of the page)
2. Drag and drop all 5 files at once:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icon-192.png`
   - `icon-512.png`
3. Scroll down, click **Commit changes**

### Step 4 — Turn on GitHub Pages
1. Click **Settings** (tab at the top of your repository)
2. Scroll down the left sidebar → click **Pages**
3. Under "Source", click the dropdown that says **None** → select **main**
4. Click **Save**
5. Wait 2–3 minutes, then refresh the page
6. You'll see a green banner: **"Your site is live at https://YOUR-USERNAME.github.io/taskpilot/"**

> 📌 Copy that URL — you'll need it for your iPhone.

---

## PART 2 — Install on Your iPhone (2 min)

### Step 5 — Add to Home Screen
1. On your iPhone, open **Safari** (must be Safari, not Chrome or Edge)
2. Go to your GitHub Pages URL: `https://YOUR-USERNAME.github.io/taskpilot/`
3. Tap the **Share** button — the box with an arrow pointing up, at the bottom of Safari
4. Scroll down in the share sheet
5. Tap **"Add to Home Screen"**
6. Name it **TaskPilot**
7. Tap **Add** (top right)
8. Go to your home screen — the TaskPilot icon will be there
9. Tap it — it opens **fullscreen**, like a native app ✓

---

## PART 3 — Get Your API Tokens (15 min total)

### Token 1 — Asana (5 min)
> This lets the app read your Asana tasks and your direct reports' tasks.

1. Go to **app.asana.com** and log in
2. Click your **profile photo** (top right)
3. Click **My Profile Settings**
4. Click the **Apps** tab
5. Click **Manage Developer Apps**
6. Click **+ New access token**
7. Name it: `TaskPilot`
8. Click **Create**
9. **Copy the token** — you won't see it again after closing
10. Open TaskPilot → tap ⚙ Settings → Asana → paste it in → tap **Save & Connect**

### Token 2 — Microsoft (Outlook + Teams) — Quick Method (5 min)
> One token covers both Outlook To-Do AND Microsoft Teams. The quick method gives you a token that lasts ~1 hour — good for testing. See "Permanent Token" below for daily use.

**Quick token (for testing):**
1. Go to **developer.microsoft.com/graph/graph-explorer**
2. Click **Sign in** (top right) → sign in with your work Microsoft account
3. Click the **Access token** tab (next to "Request")
4. Click **Copy** next to the token
5. Open TaskPilot → ⚙ Settings → Outlook + Teams → paste it in → tap **Save & Connect**

**Permanent token (recommended for daily use):**
1. Go to **portal.azure.com** and sign in
2. Search for **"App registrations"** in the top search bar
3. Click **+ New registration**
4. Name: `TaskPilot`
5. Account type: **Single tenant** (or Accounts in this org directory)
6. Redirect URI: select **Single-page application (SPA)** → enter your GitHub Pages URL: `https://YOUR-USERNAME.github.io/taskpilot/`
7. Click **Register**
8. Go to **API permissions** (left sidebar)
9. Click **+ Add a permission** → **Microsoft Graph** → **Delegated permissions**
10. Search and add each of these:
    - `Mail.Read`
    - `Tasks.ReadWrite`
    - `Team.ReadBasic.All`
    - `Channel.ReadBasic.All`
    - `ChannelMessage.Read.All`
    - `Chat.Read`
    - `User.Read`
11. Click **Grant admin consent** (if you have admin rights) or ask your IT admin
12. Copy your **Application (client) ID** from the Overview page
13. Open TaskPilot → Settings → paste the Client ID → the app will use Microsoft login to authenticate

### Token 3 — Anthropic API Key (5 min)
> This powers the AI email scanning, Teams message scanning, and WhatsApp task extraction.

1. Go to **console.anthropic.com**
2. Sign up or log in
3. Click **API Keys** (left sidebar)
4. Click **+ Create Key**
5. Name it: `TaskPilot`
6. Click **Create Key**
7. **Copy the key** — starts with `sk-ant-`
8. Open TaskPilot → ⚙ Settings → scroll to AI section → paste key → tap **Save Key**
9. Toggle **"AI email + Teams scanning"** ON

**Add credit so it works:**
1. In console.anthropic.com, click **Billing**
2. Add $5 credit (this will last 2–3 months of normal use)
3. Optional: set a monthly spending limit of $5 so there are no surprises

---

## PART 4 — Configure the App (5 min)

### Set up your Direct Reports
1. Open TaskPilot → tap ⚙ Settings
2. Scroll to **👥 Direct Reports**
3. Type the name of each person who reports to you, **exactly as their name appears in Asana**
4. Tap **Add** for each one
5. Tap the sync button (↻) — their Asana tasks will now appear with a teal "👤 Team" badge

### Select your Teams Channels
1. Open TaskPilot → tap ⚙ Settings
2. Scroll to **💬 Teams Channels**
3. Tap **Load My Channels**
4. Uncheck any channels you don't want monitored
5. Only checked channels will be scanned for tasks

### First Sync
1. Tap the **↻ sync button** in the header
2. The app will pull your Asana tasks, Outlook To-Do, and Teams messages
3. Claude will scan your emails and extract action items
4. A green dot in the header means everything synced successfully

---

## Using the App

| Feature | How to use |
|---|---|
| **Today / Week / Month / All** | Tap the view buttons below the header |
| **Filter by source** | Tap filter chips: Mine, My Team, Asana, Outlook, Teams, etc. |
| **See project details** | Tap any 📁 project name on a task card |
| **My Team tab** | Tasks assigned to your direct reports, grouped by person |
| **WhatsApp tasks** | Tap WhatsApp tab → paste any conversation → Claude extracts tasks |
| **Mark complete** | Tap the circle on any task, or open the task and tap "Mark Complete" |
| **Add manual task** | Tap the + tab (bottom right) |
| **Change theme** | ⚙ Settings → scroll to Theme → tap a colour swatch |

---

## Troubleshooting

**"The app doesn't look fullscreen on my iPhone"**
→ Make sure you're using Safari (not Chrome). Only Safari supports Add to Home Screen PWA mode.

**"Asana tasks aren't loading"**
→ Double-check your token is pasted correctly in Settings (no extra spaces). Tokens expire if you regenerate them in Asana.

**"Outlook/Teams aren't connecting"**
→ The quick Graph Explorer token expires after ~1 hour. Either get a new one or set up the permanent Azure token.

**"AI scanning isn't working"**
→ Check your Anthropic key in Settings. Make sure you have credit in your Anthropic account. Make sure "AI email + Teams scanning" toggle is ON.

**"I updated the files on GitHub but the app hasn't changed"**
→ On your iPhone, long-press the TaskPilot icon → Remove App → go back to Safari → re-add to home screen. Safari caches aggressively.

**"How do I update the app in the future?"**
→ Just replace the files on GitHub (upload new versions, commit). The app will update automatically next time you open it with an internet connection.
