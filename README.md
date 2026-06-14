# 🤖 NextHive — Human Input Interactive AI Social Media Automation

> A fully interactive, human-in-the-loop social media automation workflow built with n8n, GPT-4o, DALL·E 3, and Telegram. You stay in control — the AI does the heavy lifting.

[![n8n](https://img.shields.io/badge/Built%20with-n8n-ff6d5a?style=flat-square)](https://n8n.io)
[![GPT-4o](https://img.shields.io/badge/AI-GPT--4o-412991?style=flat-square)](https://openai.com)
[![DALL·E 3](https://img.shields.io/badge/Image-DALL·E%203-10a37f?style=flat-square)](https://openai.com)
[![Docker](https://img.shields.io/badge/Hosted-Docker-2496ED?style=flat-square)](https://docker.com)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](#)

---

## 🎯 What Makes This Different

Most automation workflows post blindly. This one **asks you first.**

Every post goes through a **3-stage human approval process** via Telegram:
1. ✅ You provide the topic and instructions
2. ✅ You approve or edit the generated content
3. ✅ You approve or regenerate the AI image

Nothing goes live without your confirmation.

---

## 🔄 How It Works

```
[Schedule — Mon & Thu 9AM]
         ↓
[Telegram → Asks you for topic + details]
         ↓
[You reply with TOPIC, AUDIENCE, TYPE, IMAGE, EXTRA]
         ↓
[Tavily → Real-time web research on your topic]
         ↓
[GPT-4o → Research Agent processes findings]
         ↓
[GPT-4o → Generates posts for all 4 platforms]
         ↓
[Telegram → Sends full content preview to you]
         ↓
    You reply: 1 (approve) / 2 (edit) / 3 (rewrite) / 4 (cancel)
         ↓
[GPT-4o → Generates perfect DALL·E 3 image prompt]
         ↓
[DALL·E 3 → Creates branded visual]
         ↓
[Telegram → Sends image preview to you]
         ↓
    You reply: 1 (approve) / 2 (retry) / 3 (custom prompt) / 4 (no image) / 5 (cancel)
         ↓
[Buffer → Posts to LinkedIn + Twitter + Instagram + Facebook]
         ↓
[Google Sheets → Logs everything]
         ↓
[Telegram → Confirms ✅]
```

---

## 💬 Telegram Conversation Example

**Bot asks:**
```
🗓️ Content Day! — Monday, June 16

TOPIC: invoice automation with n8n
AUDIENCE: business
TYPE: case_study
IMAGE: dark minimal
EXTRA: Bangladesh er small business focus korte
```

**You reply:**
```
TOPIC: invoice automation with n8n
AUDIENCE: business
TYPE: case_study
IMAGE: dark minimal
EXTRA: Bangladesh er small business focus korte
```

**Bot sends content preview → You reply `1` to approve**

**Bot sends image → You reply `1` to approve**

**Bot confirms: ✅ Published to all 4 platforms!**

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **n8n** (self-hosted, Docker) | Workflow automation engine |
| **GPT-4o** | Research agent + Content generation + Image prompt |
| **DALL·E 3** | AI image generation |
| **Tavily API** | Real-time web research |
| **Telegram Bot** | Interactive approval interface |
| **Buffer API** | Multi-platform social publishing |
| **Google Sheets** | Content log and tracking |

---

## 🧠 AI Agents Inside

### Agent 1 — Research Agent (GPT-4o)
Takes your topic and web research data → returns structured JSON with key facts, pain points, hook ideas, and source URLs.

### Agent 2 — Content Generator (GPT-4o)
Takes research JSON → generates platform-optimized posts for LinkedIn, Twitter/X, Instagram, and Facebook. Handles edit instructions too.

### Agent 3 — Image Prompt Specialist (GPT-4o)
Takes content data → generates the perfect DALL·E 3 prompt with brand colors, style, and visual concept. Provides 3 retry variations.

---

## 📋 Content Strategy

| Type | Weight | Purpose |
|------|--------|---------|
| Educational | 40% | Teach automation in simple terms |
| Inspirational | 30% | Real results, time saved, money earned |
| Case Study | 20% | Show workflows you built — attracts clients |
| Soft CTA | 10% | Invite people to work with you |

---

## 🗓️ Schedule

| Day | Time | Platforms |
|-----|------|-----------|
| Monday | 9:00 AM | LinkedIn + Twitter/X |
| Thursday | 9:00 AM | Instagram + Facebook |

**Timezone:** Asia/Dhaka (UTC+6)

---

## 🔑 Required Environment Variables

```env
OPENAI_API_KEY=your_openai_key
TAVILY_API_KEY=your_tavily_key
TELEGRAM_CHAT_ID=your_chat_id
BUFFER_ACCESS_TOKEN=your_buffer_token
BUFFER_LINKEDIN_ID=your_buffer_linkedin_profile_id
BUFFER_TWITTER_ID=your_buffer_twitter_profile_id
BUFFER_INSTAGRAM_ID=your_buffer_instagram_profile_id
BUFFER_FACEBOOK_ID=your_buffer_facebook_profile_id
GOOGLE_SHEET_ID=your_google_sheet_id
```

---

## 🚀 Setup Guide

### 1. Start n8n with Docker
```bash
docker run -d \
  --restart unless-stopped \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

### 2. Open n8n
```
http://localhost:5678
```

### 3. Import Workflow
```
Workflows → Import from File → n8n-interactive-workflow.json
```

### 4. Add Environment Variables
```
Settings → Environment Variables → Add all keys above
```

### 5. Create Telegram Bot
```
1. Open Telegram → search @BotFather
2. Send /newbot → follow steps
3. Copy Bot Token
4. Get Chat ID: https://api.telegram.org/bot<TOKEN>/getUpdates
```

### 6. Set Telegram Webhook
```
https://api.telegram.org/bot<TOKEN>/setWebhook?url=https://YOUR-N8N-URL/webhook/topic-input
```

### 7. Set Up Google Sheet
Columns needed:
```
Date | Time | Topic | Content Type | Target Audience |
LinkedIn Post | Twitter Post | Instagram Post | Facebook Post |
Image URL | Status
```

### 8. Activate Workflow
```
Toggle → Active ✅
```

---

## 📁 Project Structure

```
nexthive-social-automation/
├── n8n-interactive-workflow.json   ← Import this into n8n
├── README.md                       ← This file
├── prompts/
│   ├── research-prompt.md          ← AI Research Agent prompt
│   ├── content-prompt.md           ← Content Generation prompt
│   └── image-prompt.md             ← Image Generation prompt
└── docs/
    └── workflow-diagram.md         ← Full node explanation
```

---

## 💡 Approval Commands (Telegram)

### Content Approval:
| Reply | Action |
|-------|--------|
| `1` | Approve → go to image generation |
| `2` | Edit → tell bot what to change |
| `3` | Rewrite → same topic, fresh angle |
| `4` | Cancel → log and stop |

### Image Approval:
| Reply | Action |
|-------|--------|
| `1` | Approve → publish to all platforms |
| `2` | Retry → generate new image |
| `3` | Custom prompt → you write the prompt |
| `4` | No image → post text only |
| `5` | Cancel → stop everything |

---

## 💰 Monthly Cost Estimate

| Service | Cost |
|---------|------|
| n8n (self-hosted) | $0 |
| Tavily API | $0 (free tier) |
| Telegram Bot | $0 |
| Buffer (3 channels) | $0 (free tier) |
| Google Sheets | $0 |
| GPT-4o (~8 calls/month) | ~$0.80 |
| DALL·E 3 (~8 images/month) | ~$0.32 |
| **Total** | **~$1.12/month** |

---

## 🤝 Want This Built for Your Business?

I build custom automation workflows for businesses, agencies, and solopreneurs.

📩 monir.shazib@gmail.com
🌐 nexthiv.com
💼 linkedin.com/in/moniruzzaman-dev

---

## 📄 License

MIT License — free to use, modify, and share.

---

⭐ **If this helped you, give it a star!**
