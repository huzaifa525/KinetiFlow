# 🤖 KinetiFlow CRM

**The CRM where AI Agents do the work, you close the deals.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Stars](https://img.shields.io/github/stars/huzaifa525/KinetiFlow?style=social)](https://github.com/huzaifa525/KinetiFlow)
[![GitHub Issues](https://img.shields.io/github/issues/huzaifa525/KinetiFlow)](https://github.com/huzaifa525/KinetiFlow/issues)
[![GitHub Forks](https://img.shields.io/github/forks/huzaifa525/KinetiFlow)](https://github.com/huzaifa525/KinetiFlow/network)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue)](https://www.docker.com/)

---

## 🎯 What is KinetiFlow?

KinetiFlow is an **open-source, self-hosted, AI-powered CRM** that leverages autonomous AI agents to automate 80% of sales and relationship management tasks. Unlike traditional CRMs that require constant manual data entry, KinetiFlow uses intelligent agents that work 24/7 to:

- 🔄 **Automatically populate contact information** from emails and meetings
- 📧 **Conduct outreach and follow-ups** autonomously
- 🎤 **Transcribe and summarize meetings** in real-time
- 💚 **Monitor relationship health** and predict churn
- 📈 **Predict deal outcomes** using machine learning
- 🤝 **Handle repetitive sales tasks** so you focus on relationships

---

## ✨ Key Features

### 🆓 Free (Self-Hosted)
- ✅ **Core CRM** - Unlimited contacts, companies, and deals
- ✅ **3 AI Agents** - Email Parser, Contact Enrichment, Follow-up Reminder
- ✅ **Deal Pipelines** - Visual Kanban boards (up to 3 pipelines)
- ✅ **Activity Tracking** - Emails, calls, meetings, notes
- ✅ **Local LLM Support** - Use LLaMA, Mistral, Qwen (no OpenAI needed)
- ✅ **Gmail/Calendar Integration** - OAuth sync
- ✅ **Self-Hosted** - Your data, your infrastructure
- ✅ **API Access** - REST API for integrations

### 💎 Pro - $49/month (License Key)
- 🔓 **10+ Premium AI Agents** - Prospecting, Outreach, Voice AI, Transcription
- 🔓 **No-Code Agent Builder** - Create custom agents without coding
- 🔓 **Unlimited Pipelines & Users**
- 🔓 **Advanced Analytics** - Sales forecasting, conversion funnels
- 🔓 **Premium Integrations** - Slack, Teams, LinkedIn, Twilio
- 🔓 **White-Label Option** - Remove branding
- 🔓 **Priority Support** - 24hr email response

### 💼 Enterprise (Custom Pricing)
- 🏢 **SSO** - SAML, OKTA, Azure AD
- 🏢 **Custom Agent Development**
- 🏢 **Dedicated Account Manager**
- 🏢 **SLA Guarantee** - 99.5% uptime support
- 🏢 **Advanced RBAC** - Role-based access control

---

## 🚀 Quick Start

### Prerequisites
- Docker Desktop 24.0+
- 4GB RAM minimum (8GB recommended)
- 20GB disk space

### Installation (5 minutes)

```bash
# 1. Clone the repository
git clone https://github.com/huzaifa525/KinetiFlow.git
cd KinetiFlow

# 2. Copy environment file
cp .env.example .env

# 3. Edit configuration (optional - defaults work fine)
nano .env

# 4. Start KinetiFlow
docker-compose up -d

# 5. Open browser
http://localhost:3000

# 6. Create admin account (follow on-screen instructions)
```

That's it! Your KinetiFlow CRM is now running. 🎉

---

## 🤖 AI Agents

### Free Agents (Included)

#### 1. Email Parser Agent
Automatically monitors your connected email accounts and:
- Extracts contact information from signatures
- Detects new leads and opportunities
- Creates/updates contacts without manual entry
- Identifies potential deals from conversations

#### 2. Contact Enrichment Agent
Enriches your contacts with:
- LinkedIn profiles and job titles
- Company information (size, industry, revenue)
- Social media profiles
- Missing contact details

#### 3. Follow-up Reminder Agent
Keeps relationships warm by:
- Tracking last contact date
- Sending timely reminders (7, 14, 30 days)
- Suggesting follow-up messages
- Preventing relationships from going cold

### Premium Agents (Pro License Required) 🔑

#### 4. Prospecting Agent
Finds new leads automatically:
- Scrapes LinkedIn and industry directories
- Qualifies leads based on your criteria
- Enriches with contact information
- Adds to pipeline automatically

#### 5. Outreach Agent
Automates email campaigns:
- Writes personalized emails
- A/B tests different approaches
- Handles follow-up sequences
- Learns your writing style

#### 6. Meeting Transcription Agent
Captures every meeting detail:
- Real-time transcription (Zoom, Meet, Teams)
- Extracts action items and next steps
- Summarizes key discussion points
- Updates CRM automatically

#### 7. Voice AI Agent
Makes and receives calls:
- Outbound qualifying calls
- Handles basic customer questions
- Books appointments over phone
- Multi-language support (50+ languages)

#### 8. Deal Progression Agent
Moves deals forward autonomously:
- Monitors deal activity
- Identifies stalled deals
- Suggests actions to progress deals
- Predicts close probability

#### 9. Sentiment Analysis Agent
Monitors relationship health:
- Analyzes tone in communications
- Detects tone shifts (red flags)
- Tracks customer satisfaction
- Alerts on at-risk relationships

#### 10. Competitive Intelligence Agent
Stays ahead of competition:
- Monitors competitor mentions
- Tracks pricing changes
- Alerts on competitive threats
- Provides talking points

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────┐
│           Next.js Frontend (Web UI)         │
└─────────────────┬───────────────────────────┘
                  │
         ┌────────▼────────┐
         │   Nginx Proxy   │
         └────────┬────────┘
                  │
    ┌─────────────┴─────────────┐
    │                           │
┌───▼────────┐         ┌────────▼──────┐
│  FastAPI   │         │   WebSocket   │
│  Backend   │         │    Server     │
└───┬────────┘         └───────────────┘
    │
    ├─────────┬──────────┬──────────┐
    │         │          │          │
┌───▼───┐ ┌──▼──┐ ┌─────▼────┐ ┌──▼────────┐
│ PostgreSQL│Redis│ Weaviate │ │Celery     │
│  +pgvector│Cache│ Vector DB│ │Workers    │
└───────┘ └─────┘ └──────────┘ └───┬───────┘
                                    │
                            ┌───────▼───────┐
                            │   AI Agents   │
                            │  (LangGraph)  │
                            └───────────────┘
```

---

## 💻 Tech Stack

### Frontend
- **Next.js 14** - React framework with App Router
- **TypeScript** - Type safety
- **TailwindCSS** - Utility-first CSS
- **Shadcn UI** - Beautiful components
- **Zustand** - State management
- **React Query** - Data fetching

### Backend
- **FastAPI** - Modern Python web framework
- **PostgreSQL 16** - Primary database with pgvector
- **Redis 7** - Cache and task queue
- **Weaviate** - Vector database for AI
- **Celery** - Background job processing
- **SQLAlchemy** - ORM
- **Alembic** - Database migrations

### AI/ML
- **LangGraph** - Agent orchestration framework
- **LangChain** - LLM tooling
- **OpenAI GPT-4** - Premium AI (optional)
- **LLaMA 3.2** - Self-hosted AI (free)
- **Mistral** - Self-hosted AI (free)
- **Whisper** - Speech-to-text
- **HuggingFace** - Model library

### DevOps
- **Docker & Docker Compose** - Containerization
- **Nginx** - Reverse proxy
- **GitHub Actions** - CI/CD
- **Let's Encrypt** - SSL certificates

---

## 📖 Documentation

- **Full Documentation:** [docs.KinetiFlow.com](https://docs.KinetiFlow.com) (Coming soon)
- **API Reference:** [api.KinetiFlow.com](https://api.KinetiFlow.com) (Coming soon)
- **Agent Development Guide:** [See Wiki](https://github.com/huzaifa525/KinetiFlow/wiki)

---

## 🌟 Why KinetiFlow?

### vs. Salesforce/HubSpot
- ✅ **90% cheaper** - $49 flat vs $75-300/user/month
- ✅ **True agentic AI** - Not just automation
- ✅ **Self-hosted** - Your data, your control
- ✅ **No vendor lock-in** - Open source

### vs. Open Source CRMs
- ✅ **AI-first design** - Built for autonomous agents
- ✅ **Modern stack** - FastAPI/Next.js vs PHP
- ✅ **Agent marketplace** - Extensible ecosystem
- ✅ **Better DX** - Developer-friendly APIs

### vs. Traditional CRMs
- ✅ **Zero data entry** - Agents populate CRM automatically
- ✅ **24/7 automation** - Agents work while you sleep
- ✅ **Privacy-first** - Local LLMs, no cloud dependency
- ✅ **Customizable** - Build your own agents

---

## 🗺️ Roadmap

### ✅ Phase 1: MVP (Q4-Q1 2025-2026)
- [x] Core CRM features
- [x] 3 free AI agents
- [x] License key system
- [ ] Docker deployment
- [ ] Documentation
- [ ] Product Hunt launch

### 🚧 Phase 2: Intelligence (Q2-Q3 2026)
- [ ] 10+ premium agents
- [ ] No-code agent builder
- [ ] Agent marketplace (beta)
- [ ] Voice AI agents
- [ ] Multi-agent orchestration

### 📅 Phase 3: Scale (Q4-Q5 2026)
- [ ] Enterprise features (SSO, RBAC)
- [ ] Industry agent packs (Medical, Real Estate, SaaS)
- [ ] Mobile apps (iOS/Android)
- [ ] Cloud-hosted option

### 🔮 Phase 4: Platform (2027)
- [ ] Agent SDK (Python/TypeScript/Go)
- [ ] Public API v2 (GraphQL)
- [ ] Advanced integrations
- [ ] Multi-modal AI agents

---

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.

### Ways to Contribute
- 🐛 Report bugs
- 💡 Suggest features
- 📝 Improve documentation
- 🔧 Submit pull requests
- 🤖 Build custom agents
- 🌍 Translate to other languages

---

## 📄 License

KinetiFlow is open source under the [MIT License](LICENSE).

```
Copyright (c) 2025 Huzefa Nalkheda Wala

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

See [LICENSE](LICENSE) for full text.

---

## 💬 Community & Support

- **Discord:** [discord.gg/KinetiFlow](https://discord.gg/KinetiFlow) (Coming soon)
- **GitHub Discussions:** [Ask questions](https://github.com/huzaifa525/KinetiFlow/discussions)
- **Twitter:** [@KinetiFlowcrm](https://twitter.com/KinetiFlowcrm) (Coming soon)
- **Email:** support@KinetiFlow.com (Coming soon)

---

## 🙏 Acknowledgments

Built with amazing open-source tools:
- [FastAPI](https://fastapi.tiangolo.com/)
- [Next.js](https://nextjs.org/)
- [LangChain](https://langchain.com/)
- [PostgreSQL](https://www.postgresql.org/)
- [Shadcn UI](https://ui.shadcn.com/)

---

## ⭐ Star History

[![Star History Chart](https://api.star-history.com/svg?repos=huzaifa525/KinetiFlow&type=Date)](https://star-history.com/#huzaifa525/KinetiFlow&Date)

---

## 📊 Status

**Current Version:** v0.1.0 (Pre-Alpha)
**Status:** 🚧 Under Active Development
**Next Milestone:** MVP Launch (March 2025)

---

<div align="center">

**Made with ❤️ by [Huzefa Nalkheda Wala](https://github.com/huzaifa525)**

**[⭐ Star us on GitHub](https://github.com/huzaifa525/KinetiFlow) • [🐛 Report Bug](https://github.com/huzaifa525/KinetiFlow/issues) • [💡 Request Feature](https://github.com/huzaifa525/KinetiFlow/issues)**

</div>
