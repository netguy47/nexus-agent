# NEXUS Chrome Extension
### AI Agent for Freelance, Email, Docs & Antigravity Bridge

---

## QUICK START (Load in Chrome)

1. Open Chrome → navigate to `chrome://extensions`
2. Enable **Developer Mode** (top-right toggle)
3. Click **"Load unpacked"**
4. Select this `nexus-extension/` folder
5. The NEXUS icon appears in your toolbar

---

## FIRST-TIME SETUP

### 1. Add your Anthropic API Key
- Click the NEXUS toolbar icon
- Click **Settings** → enter your `sk-ant-api03-...` key → Save

### 2. Connect Google Account (for Gmail + Drive)
- In Settings tab → click **"CONNECT GOOGLE"**
- Approve the OAuth permissions popup
- You'll see "✓ Connected to Google"

### 3. Set Antigravity Bridge URL (optional)
- In Settings tab → enter your backend URL
- Format: `https://your-bridge-domain.com/api`

---

## HOW TO USE

### On Upwork / Fiverr / Freelancer
1. Open any job posting
2. The **NX** tab appears on the right edge of the screen
3. Click it to open the sidebar
4. Hit **"ANALYZE JOB"** → get requirements, red flags, fit score
5. Hit **"DRAFT PROPOSAL"** → get a ready-to-submit proposal
6. Hit **"▶ AUTO-FILL"** → fills the proposal field automatically
7. Use **SEND / SAVE** to save to Google Drive

### On Gmail
1. Open an email or thread
2. Open NEXUS sidebar
3. Hit **"SUMMARIZE"** → get thread summary + action items
4. Hit **"DRAFT REPLY"** → get a ready-to-send reply
5. Use **SEND / SAVE** → sends via Gmail API directly

### On LinkedIn / Indeed
1. Open a job listing
2. NEXUS analyzes requirements and generates a tailored cover letter

### Antigravity Bridge
- On any Google Doc or Drive page, hit **"◈ ANTIGRAVITY"**
- Saves context to Drive and syncs with your bridge endpoint
- Chat with NEXUS to coordinate research pipeline tasks

---

## FILE STRUCTURE
```
nexus-extension/
├── manifest.json          Chrome Extension config
├── src/
│   ├── background.js      Service worker: API, OAuth, Gmail, Drive
│   ├── content.js         Injected into pages: sidebar + DOM bridge
│   ├── sidebar.css        Host-page styles for the NX tab + iframe
│   ├── sidebar.html       Full NEXUS agent UI (runs in iframe)
│   └── popup.html         Toolbar icon popup
└── icons/
    ├── icon16.png         (add your own 16×16 icon)
    ├── icon48.png         (add your own 48×48 icon)
    └── icon128.png        (add your own 128×128 icon)
```

---

## GOOGLE OAUTH SETUP (for Gmail/Drive)

1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a project → Enable **Gmail API** and **Google Drive API** and **Google Docs API**
3. Go to **OAuth consent screen** → set up as "External"
4. Create **OAuth 2.0 Credentials** → type: **Chrome Extension**
5. Copy the **Client ID** → paste into `manifest.json` under `oauth2.client_id`
6. Reload the extension

---

## ANTIGRAVITY BRIDGE API CONTRACT

NEXUS expects these endpoints on your bridge server:

```
POST /api/memory          { text, source, tags[] }
POST /api/drive/save      { title, content, folder }
POST /api/pipeline/ingest { url, context, type }
GET  /api/pipeline/status
```

All requests include header: `X-Nexus-Session: <sessionId>`

---

## ADDING ICONS

Create 3 PNG icons and place in `icons/`:
- `icon16.png`  — 16×16px
- `icon48.png`  — 48×48px  
- `icon128.png` — 128×128px

Quick way: use any favicon generator online with the text "NX" on a dark background.

Or remove the `default_icon` block from manifest.json temporarily.

---

## KNOWN LIMITATIONS

| Feature | Status |
|---|---|
| Upwork auto-fill | ✅ Works (selector-based) |
| Gmail send | ✅ Works (OAuth required) |
| Drive save | ✅ Works (OAuth required) |
| Fiverr auto-fill | ✅ Works |
| LinkedIn Easy Apply | ⚠ Partial (form varies) |
| NotebookLM direct API | ❌ No public API — use bridge |
| Web search | ⚠ Requires backend proxy |

---

## SUPPORT

Built by NEXUS / Don — part of the Antigravity project stack.
