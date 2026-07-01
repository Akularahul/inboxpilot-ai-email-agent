<!-- Header -->
<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:0f0c29,50:302b63,100:24243e&height=200&section=header&text=InboxPilot&fontSize=60&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=Autonomous%20AI%20Email%20Operations%20Agent%20·%20Claude%20·%20LangGraph%20·%20MCP&descSize=16&descAlignY=60&descColor=a5b4fc" />

<div align="center">

![Claude](https://img.shields.io/badge/Claude-D97757?style=flat-square&logo=anthropic&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![MCP](https://img.shields.io/badge/MCP-000000?style=flat-square&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Salesforce](https://img.shields.io/badge/Salesforce-00A1E0?style=flat-square&logo=salesforce&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-22c55e?style=flat-square)

</div>

## ◈ Overview

**InboxPilot** is an autonomous, always-on AI agent that turns a chaotic inbox into a clean, prioritized operations feed. It monitors email **24/7** via the Gmail API, uses **Claude** to classify, summarize, and extract action items from every message, and delivers a scheduled **8 AM executive digest** to **Notion** and **Slack**. Its differentiator: it reaches into **Salesforce** to auto-create Leads and log activities — extending Agentforce-style automation from CRM into everyday work.

> Not "another email summarizer" — an agent that runs your email operations while you sleep.

## ◈ What It Does

1. **📡 Monitors** — watches the inbox in real time via Gmail API push notifications
2. **🏷️ Classifies & prioritizes** — urgent / action-needed / FYI / noise, with a priority score
3. **📝 Summarizes** — a 2-line TL;DR plus extracted action items, deadlines, people, and amounts
4. **✍️ Drafts replies** — suggests context-aware responses for approval
5. **🗂️ Logs to Notion** — writes a structured record to a Notion database
6. **📨 Morning digest** — delivers "the 6 things that matter today" to Notion & Slack at 8 AM
7. **🔗 Syncs to Salesforce** — auto-creates Leads / logs activities for customer emails via REST API

## ◈ Architecture

```
                    ┌─────────────────────────┐
   Gmail API  ─────▶│   LangGraph Orchestrator │◀──── Scheduler (8 AM digest)
   (push)           └───────────┬─────────────┘
                                │
              ┌─────────────────┼──────────────────┐
              ▼                 ▼                  ▼
       Classify Agent    Summarize Agent     Action Agent
         (Claude)          (Claude)            (Claude)
              │                 │                  │
              └───────┬─────────┴──────────┬───────┘
                      ▼                     ▼
              RAG / Vector Memory     MCP Tool Servers
              (thread context)     (Gmail · Notion · Slack)
                      │                     │
                      ▼                     ▼
                Notion Database   ──▶  Salesforce REST API
                Slack Digest             (Leads / Activities)
```

## ◈ Tech Stack

| Layer | Technology |
|---|---|
| Reasoning / LLM | Claude (Anthropic API) |
| Agent orchestration | LangGraph |
| Tool integration | MCP (Model Context Protocol) — Gmail, Notion, Slack servers |
| Email (real-time) | Gmail API + Pub/Sub push |
| Memory / context | RAG with vector store (Chroma) |
| CRM sync | Salesforce REST API |
| Backend | Python, FastAPI (async) |
| Scheduling / deploy | Cron / AWS Lambda, Docker |

## ◈ Project Structure

```
inboxpilot/
├── agents/            # Classify, summarize, and action agents
├── mcp_servers/       # Gmail, Notion, and Slack MCP integrations
├── memory/            # RAG vector store + thread context
├── integrations/      # Salesforce REST client
├── digest/            # 8 AM digest builder & scheduler
├── prompts/           # Structured Claude prompts (JSON tool calling)
└── app.py             # FastAPI entrypoint
```

## ◈ Getting Started

```bash
# Clone and install
git clone https://github.com/Akularahul/inboxpilot-ai-email-agent.git
cd inboxpilot-ai-email-agent
pip install -r requirements.txt

# Configure secrets
cp .env.example .env      # ANTHROPIC_API_KEY, GMAIL creds, NOTION_TOKEN, SF creds

# Run the agent
python app.py
```

## ◈ Roadmap

- [ ] Voice digest via text-to-speech
- [ ] Auto-scheduling of meetings from detected requests
- [ ] Multi-account (Gmail + Outlook) support
- [ ] Agentforce action integration inside Salesforce

---

<div align="center">

**Built by Rahul Akula** · Salesforce Certified Administrator & Agentforce Specialist

<a href="https://www.linkedin.com/in/rahul-akula-0a0284310"><img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin&logoColor=white"/></a>
&nbsp;
<a href="mailto:akula.rahul4545@gmail.com"><img src="https://img.shields.io/badge/Email-Say%20Hello-EA4335?style=flat-square&logo=gmail&logoColor=white"/></a>

</div>
