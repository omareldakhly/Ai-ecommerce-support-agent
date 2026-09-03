# AI E-Commerce Support Agent — Case Study

> **Project:** AI E-Commerce Support Agent  
> **Platform:** n8n  
> **AI Model:** OpenAI GPT-4.1-mini  
> **Date:** September 2026  
> **Developer:** Omar Mohamed — AI Automation Specialist

*Part of the [AI E-Commerce Support Agent](./README.md) repository.*

---

## The Problem

E-commerce stores handle hundreds of customer inquiries daily across multiple channels — product questions, shipping policies, order status checks, complaints, and refund requests. Manual handling leads to:

- **Slow response times** (30–60 minutes average)
- **Missed complaints** and unresolved tickets
- **Inconsistent answers** to policy questions
- **No audit trail** of customer conversations
- **Support team burnout** from repetitive queries

---

## The Solution

An AI-powered customer support agent built on **n8n** that operates 24/7 via **Telegram**, integrating multiple tools to handle inquiries end-to-end:

### Core Components

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Trigger** | Telegram Bot Webhook | Receives customer messages instantly |
| **AI Brain** | GPT-4.1-mini + Conversation Memory | Understands intent, maintains context |
| **Knowledge Base** | Supabase Vector Store (RAG) | Retrieves company policies instantly |
| **Order Lookup** | Google Sheets Tool | Real-time order status queries |
| **Ticket System** | Google Sheets Append | Auto-creates support tickets |
| **Admin Alerts** | Telegram Bot | Notifies human team for escalations |
| **Audit Log** | Google Sheets | Logs every conversation for review |

### Key Features

1. **RAG-Powered Policy Answers** — Company policies (shipping, returns, payments) are embedded in Supabase Vector Store. The AI retrieves exact policy text instead of hallucinating answers.

2. **Real-Time Order Tracking** — Customers mention their order ID, and the AI queries Google Sheets to return live status updates.

3. **Smart Escalation** — When a complaint requires human intervention (damaged product, refund request, angry customer), the AI auto-creates a ticket and alerts the admin via Telegram.

4. **Conversation Memory** — The agent remembers previous messages in the same chat session, enabling natural multi-turn conversations.

5. **Security Guardrails** — Strict system prompt prevents prompt injection, data leakage, and unauthorized access to bulk customer data.

6. **Full Audit Trail** — Every customer message, AI reply, and escalation is logged to Google Sheets with timestamps for compliance and quality review.

---

## Architecture Diagram

![Architecture Diagram](./assets/ai-ecommerce-support-architecture.png)

### Data Flow

```
Customer (Telegram) 
    ↓
Telegram Trigger (Webhook)
    ↓
AI Agent (GPT-4.1-mini + Memory)
    ├──→ Supabase Vector Store — Policy lookup (RAG)
    ├──→ Google Sheets — Order status query
    ├──→ Google Sheets — Ticket creation (escalations)
    ├──→ Google Sheets — Conversation logging
    └──→ Telegram Bot — Admin alert (if escalated)
    ↓
Send Reply (Telegram Bot)
```

---

## The Results

| Metric | Before | After |
|--------|--------|-------|
| Response Time | 30–60 min | **5–10 seconds** |
| Policy Answer Accuracy | Inconsistent | **RAG-grounded — every answer traces back to a real policy doc** |
| Missed Complaints | Common | **Zero in testing** (auto-ticketed) |
| Admin Alert Speed | Manual discovery | **Instant** |
| Audit Trail | None | **Complete conversation log** |
| Support Hours | Business hours only | **24/7** |

*Results measured during development/testing on a representative set of customer scenarios, not yet at full production volume.*

---

## Technical Highlights

### RAG Implementation
- Company policies stored as text files
- OpenAI embeddings (`text-embedding-3-small`) generate vectors
- Supabase Vector Store enables semantic similarity search
- AI retrieves only relevant policy sections per query

### Security Measures
- System prompt includes strict guardrails against:
  - Prompt injection attacks
  - System prompt extraction attempts
  - Bulk data requests ("show all orders")
  - Policy override attempts
- All data access is tool-mediated — AI never "guesses"

### Error Handling
- n8n error branches catch API failures
- Fallback messages inform customers when systems are down
- Retry logic on transient failures

---

## Tools & Integrations

- **n8n** — Workflow automation platform
- **OpenAI GPT-4.1-mini** — Language model
- **Supabase** — Vector database for RAG
- **Google Sheets** — Order data, tickets, conversation logs
- **Telegram Bot API** — Customer interface + admin alerts
- **OpenAI Embeddings** — Vector generation for RAG

---

## What I Learned

This was my **first n8n project**, and it taught me:
- How to structure AI agents with tool-calling in n8n
- The power of RAG for grounding AI responses in real documents
- The importance of conversation memory for natural UX
- How to build security guardrails directly into the system prompt
- The value of audit logging for production AI systems

---

## Next Steps

- [ ] Add voice message support (Whisper transcription)
- [ ] Multi-language support (Arabic + English)
- [ ] Integration with Shopify/WooCommerce for live inventory
- [ ] Sentiment analysis for proactive escalation
- [ ] Dashboard for admin to monitor ticket queue

---

## Connect With Me

- **LinkedIn:** [Omar Mohamed](https://www.linkedin.com/in/omar-mohamed-267361418/)
- **GitHub:** [omareldakhly](https://github.com/omareldakhly)
- **Email:** omareldakhly20@gmail.com
- **WhatsApp:** [+20 112 715 4991](https://wa.me/201127154991)

---

*Built with n8n, OpenAI, and a lot of coffee ☕*
