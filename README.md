# n8n Enterprise Workshop

A hands-on workshop project for learning n8n workflow automation with AI-powered bots (Slack & Telegram), MCP integration, and Claude AI assistance.

---

## 📁 Project Structure

```
n8n/
├── $.mcp.json                  # MCP config template (fill in your credentials)
├── .claude/                    # Claude AI configuration
│   ├── settings.json           # Claude hooks for n8n workflow tools
│   ├── n8n-mcp-start.sh        # Script to launch n8n-mcp server (reads from .env)
│   └── skills/                 # Claude skill pack symlink → n8n-skills
├── n8n-skills/                 # n8n skill reference pack
│   ├── SKILL.md                # Skill pack overview
│   └── resources/              # Node references, workflow patterns, templates
│       ├── INDEX.md            # Full node index
│       ├── compatibility-matrix.md
│       ├── input/              # Input node guides
│       ├── output/             # Output node guides
│       ├── transform/          # Data transform node guides
│       ├── trigger/            # Trigger node guides
│       ├── guides/             # General workflow guides
│       ├── templates/          # Reusable workflow templates
│       └── ...
├── template_no_creds/          # Sanitized workflow JSON files (credential-free)
│   ├── Learn_n8n.json          # Introductory learning workflow
│   ├── Slack_RAG_bot_v1.json   # Slack RAG bot (version 1)
│   ├── Slack_RAG_bot_v2.json   # Slack RAG bot (version 2, improved)
│   ├── Telegram_AI_bot_v1.json # Telegram AI chatbot (version 1)
│   └── Telegram_AI_bot_v2.json # Telegram AI chatbot (version 2, with image gen)
├── docs/                       # Course lecture materials
│   └── 講義/                   # Session handouts & slides
├── CLAUDE.md                   # Claude AI rules for n8n JSON generation
└── .gitignore
```

---

## 🚀 Getting Started

### 1. Set up credentials

Copy the MCP config template and fill in your own values:

```bash
cp $.mcp.json .mcp.json
```

Then edit `.mcp.json` with:
- `N8N_API_URL` → your ngrok URL (e.g. `https://xxx.ngrok-free.dev`)
- `N8N_API_KEY` → your n8n API key from **Settings → API**

Also create a `.env` file in the project root:

```
ngrok = YOUR_NGROK_AUTHTOKEN
n8n_api = YOUR_N8N_API_KEY
```

### 2. Start n8n locally (Docker)

```bash
docker run -it --rm \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

### 3. Expose n8n with ngrok

```bash
ngrok http --url=YOUR_NGROK_DOMAIN 5678
```

### 4. Import a workflow

Go to n8n → **Workflows → Import from file**, then select any JSON from `template_no_creds/`.  
After import, re-configure the credential nodes in the UI.

---

## 🤖 Claude + MCP Integration

This project uses [n8n-mcp](https://github.com/czlonkowski/n8n-mcp) to let Claude AI directly manage your n8n workflows.

The `.claude/n8n-mcp-start.sh` script reads credentials from `.env` and launches the MCP server automatically when you start a Claude session.

Claude hooks are pre-configured in `.claude/settings.json` to:
- Load node documentation before looking up nodes
- Validate workflows before saving
- Apply n8n-skills patterns during workflow creation

---

## 📦 Workflow Templates

| File | Description |
|------|-------------|
| `Learn_n8n.json` | Beginner workflow covering core n8n concepts |
| `Slack_RAG_bot_v1.json` | Slack bot with RAG (Retrieval-Augmented Generation) |
| `Slack_RAG_bot_v2.json` | Improved Slack RAG bot with better error handling |
| `Telegram_AI_bot_v1.json` | Telegram chatbot powered by AI |
| `Telegram_AI_bot_v2.json` | Telegram bot with AI image generation support |

> All templates have credentials removed. You will need to re-link credentials after importing into your n8n instance.

---

