# 🛡 IdentityGuard — DEVONN LYNCH
## Deployment Guide: Vercel (Option A) + OpenClaw (Option B)

---

## OPTION A — VERCEL (Live web app, ~10 minutes)

### Prerequisites
- A GitHub account (free): github.com
- A Vercel account (free): vercel.com
- Your Anthropic API key: console.anthropic.com/settings/keys

---

### Step 1 — Upload to GitHub

1. Go to **github.com/new** → create a new repo named `identityguard`
2. Upload all files from this folder (drag and drop, or use GitHub Desktop)
3. Make sure the repo is **Private**

Your repo should have:
```
identityguard/
├── api/
│   └── chat.js          ← Secure API proxy (hides your key)
├── src/
│   └── index.html       ← The full app
├── vercel.json          ← Deployment config
├── package.json
├── .gitignore
└── .env.example
```

---

### Step 2 — Deploy on Vercel

1. Go to **vercel.com/new**
2. Click **"Import Git Repository"** → select your `identityguard` repo
3. Leave all settings as default
4. Before clicking Deploy, click **"Environment Variables"** and add:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** `sk-ant-your-actual-key-here`
5. Click **Deploy**

✅ In ~60 seconds you'll have a live URL like:
`https://identityguard-devonnlynch.vercel.app`

---

### Step 3 — Test It

1. Open your Vercel URL
2. Click any Quick Action button
3. You should get a real AI response within 3-5 seconds

---

### Your API Key Is Secure
- The key lives only in Vercel's encrypted environment variables
- It is NEVER exposed in the browser or frontend code
- All AI calls go through `/api/chat.js` on the server

---

## OPTION B — OPENCLAW (Self-hosted AI agent, phone/desktop access)

OpenClaw lets you talk to your IdentityGuard agent via WhatsApp, Telegram, iMessage, Discord, Slack, and more — from any device.

### Prerequisites
- Node.js 24: nodejs.org/en/download
- Your Anthropic API key

---

### Step 1 — Install OpenClaw

**macOS / Linux:**
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

**Windows (PowerShell as Admin):**
```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

---

### Step 2 — Run Onboarding

```bash
openclaw onboard --install-daemon
```

When prompted:
- **Model provider:** Anthropic
- **API key:** paste your `sk-ant-...` key
- **Model:** claude-sonnet-4-20250514

---

### Step 3 — Apply IdentityGuard Config

Copy `openclaw/openclaw.json` to your OpenClaw config directory:

```bash
# macOS/Linux:
cp openclaw/openclaw.json ~/.openclaw/openclaw.json

# Windows:
copy openclaw\openclaw.json %USERPROFILE%\.openclaw\openclaw.json
```

Edit `~/.openclaw/openclaw.json` and fill in:
- `YOUR_PHONE_NUMBER_E164_FORMAT` → e.g. `+15555550100`
- `YOUR_TELEGRAM_USERNAME` → e.g. `devonnlynch`

---

### Step 4 — Start the Gateway

```bash
openclaw gateway start
openclaw dashboard
```

Opens at: `http://127.0.0.1:18789`

---

### Step 5 — Connect a Channel (Optional — chat from phone)

**Fastest option — Telegram:**
1. Message @BotFather on Telegram → create a new bot
2. Copy the bot token
3. Run: `openclaw onboard --channel telegram`
4. Paste your token
5. Message your bot from Telegram — IdentityGuard responds instantly

**WhatsApp:** See docs.openclaw.ai/channels/whatsapp
**iMessage:** See docs.openclaw.ai/channels/imessage (macOS only)

---

## BOTH OPTIONS ACTIVE = Maximum Coverage

| | Option A (Vercel) | Option B (OpenClaw) |
|---|---|---|
| Access | Browser, any device | WhatsApp, Telegram, iMessage, Slack |
| Hosting | Vercel cloud | Your machine or server |
| API key | Vercel env var | OpenClaw config |
| Always on | Yes (Vercel) | While Gateway is running |
| Phone access | Yes (browser) | Yes (native messaging apps) |

---

## Security Reminders
- ⚠️ Never commit your `.env` file or API key to GitHub
- 🔐 Never type your full SSN into any chat window
- 🛡 Legal name is always: **DEVONN LYNCH** (two N's, no middle name)

---

*Built by Devonn Lynch + Claude · IdentityGuard v1.0*
