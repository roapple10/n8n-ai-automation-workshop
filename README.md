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
├── n8n_template/               # Sanitized workflow JSON files (credential-free)
│   ├── Learn_n8n.json          # Introductory learning workflow
│   ├── Slack_practice/         # Slack automation practice workflows
│   │   ├── 01_slack_weekly_summary.json
│   │   ├── 02_gmail_ai_classify_slack.json
│   │   ├── 03_email_ai_agent_slack.json
│   │   ├── 04_Slack RAG Agent(AI Router + Thinking Ack).json
│   │   └── Slack Project Update RAG Agent.json
│   ├── Telegram_practice/      # Telegram bot practice workflows
│   │   ├── 01_expense_tracker_telegram_sheets.json
│   │   ├── 02_task_manager_telegram_sheets.json
│   │   ├── 03_image_generator_dalle_telegram.json
│   │   ├── 04_content_script_generator_telegram.json
│   │   └── Telegram AI-bot.json
│   └── Sample_data/            # Sample CSV / GSheet files for practice
│       ├── 01_expense_tracker_sample.*
│       ├── 02_task_manager_sample.*
│       ├── 03_image_log_sample.*
│       ├── 04_slack_stars_sample.*
│       └── 05_job_tracker_sample.*
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

Go to n8n → **Workflows → Import from file**, then select any JSON from `n8n_template/`.  
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

### General

| File | Description |
|------|-------------|
| `Learn_n8n.json` | Beginner workflow covering core n8n concepts |

### Slack Practice (`Slack_practice/`)

| File | Description |
|------|-------------|
| `01_slack_weekly_summary.json` | Auto-generate weekly summaries and post to Slack |
| `02_gmail_ai_classify_slack.json` | AI classifies Gmail and forwards to Slack channels |
| `03_email_ai_agent_slack.json` | Email AI agent with Slack notification |
| `04_Slack RAG Agent(AI Router + Thinking Ack).json` | Slack RAG bot with AI router and thinking acknowledgement |
| `Slack Project Update RAG Agent.json` | Slack bot for project update RAG queries |

### Telegram Practice (`Telegram_practice/`)

| File | Description |
|------|-------------|
| `01_expense_tracker_telegram_sheets.json` | Log expenses via Telegram, sync to Google Sheets |
| `02_task_manager_telegram_sheets.json` | Manage tasks via Telegram, sync to Google Sheets |
| `03_image_generator_dalle_telegram.json` | Generate DALL-E images via Telegram bot |
| `04_content_script_generator_telegram.json` | Generate content scripts via Telegram |
| `Telegram AI-bot.json` | General-purpose Telegram AI chatbot |

### Sample Data (`Sample_data/`)

| Dataset | Description |
|---------|-------------|
| `01_expense_tracker_sample` | Sample expense records |
| `02_task_manager_sample` | Sample task list |
| `03_image_log_sample` | Sample image generation log |
| `04_slack_stars_sample` | Sample Slack starred messages |
| `05_job_tracker_sample` | Sample job application tracker |

> All templates have credentials removed. You will need to re-link credentials after importing into your n8n instance.

---

