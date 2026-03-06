<div align="center">

# 🤖 Agentic Customer Care AI

### _Where AI Agents Think, Collaborate, and Solve Customer Problems Autonomously_

<br />

<img src="https://img.shields.io/badge/LangGraph-Multi--Agent_System-FF6B35?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0id2hpdGUiPjxwYXRoIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyem0wIDE4Yy00LjQyIDAtOC0zLjU4LTgtOHMzLjU4LTggOC04IDggMy41OCA4IDgtMy41OCA4LTggOHoiLz48L3N2Zz4=&logoColor=white" alt="LangGraph" />
<img src="https://img.shields.io/badge/GPT--4o-Powered-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI" />
<img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI" />
<img src="https://img.shields.io/badge/Next.js_16-000000?style=for-the-badge&logo=next.js&logoColor=white" alt="Next.js" />
<img src="https://img.shields.io/badge/React_19-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React" />
<img src="https://img.shields.io/badge/Python_3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
<img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />

<br />
<br />

**5 AI Agents** · **3 Safety Guardrails** · **11 Autonomous Tools** · **1M+ Orders Tested**

[Features](#-the-agents) · [Architecture](#-architecture) · [Quick Start](#-quick-start) · [Try It](#-try-it) · [Deploy Free](#-deploy-for-free)

<br />

---

</div>

<br />

## 💡 What Is This?

Imagine a customer care system where **AI agents don't just answer questions — they think, reason, use tools, and collaborate** to solve problems. No scripts. No decision trees. Just autonomous agents that understand context and take action.

```
Customer: "I bought a Garmin watch last week but it's too big.
           Can I return it? I have the box and everything."

🧠 Router Agent    → Detects return intent (confidence: 0.96)
📦 Returns Agent   → Looks up order → Finds Garmin Watch (Product #21)
                   → Checks return policy → Sports: 45-day window ✓
                   → Calculates refund → $449.99 (0% restocking fee)
                   → "Great news! Your Garmin Forerunner 265 is eligible..."
```

Every response is **validated through 3 guardrail layers** — prompt injection detection, PII redaction, and policy compliance checks — before reaching the customer.

<br />

## 🎯 The Agents

<table>
<tr>
<td width="50%">

### 🔀 Router Agent
**The Brain — Intent Classification**

Analyzes every incoming message and routes to the right specialist. Uses LLM-powered JSON classification with confidence scoring. If confidence < 60%, asks for clarification instead of guessing.

**Handles:** Greetings, goodbyes, ambiguous queries

</td>
<td width="50%">

### 🔍 Product Specialist
**Your Personal Shopping Assistant**

Searches the catalog, compares products side-by-side, and makes recommendations based on what you need. Knows specs, prices, ratings, and stock levels.

**Tools:** `search_products` · `get_product_details` · `compare_products`

</td>
</tr>
<tr>
<td width="50%">

### 📦 Order Tracker
**Real-Time Shipment Intelligence**

Tracks orders across all statuses — from confirmed to delivered. Provides tracking numbers, carrier info, and estimated delivery dates. Can pull up your full order history instantly.

**Tools:** `lookup_order` · `get_order_status` · `get_user_orders`

</td>
<td width="50%">

### ↩️ Returns Specialist
**Policy Expert + Refund Calculator**

Looks up orders, identifies products, checks return eligibility against category-specific policies, calculates restocking fees, and initiates return requests — all autonomously.

**Tools:** `lookup_order` · `check_return_eligibility` · `initiate_return`

</td>
</tr>
<tr>
<td colspan="2" align="center">

### 🚨 Escalation Handler
**The Empathy Engine**

Detects frustration, requests for human agents, or multi-domain issues. Generates an empathetic response AND a detailed handoff summary for the human agent — including conversation context, emotional state, and priority level.

</td>
</tr>
</table>

<br />

## 🏗 Architecture

```
                              ┌─────────────────┐
                              │   Customer Chat  │
                              │   (Next.js 16)   │
                              └────────┬─────────┘
                                       │
                                       ▼
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│   ┌──────────────┐         LANGGRAPH ORCHESTRATOR                    │
│   │    INPUT      │                                                   │
│   │  GUARDRAIL    │    ┌──────────────────────────────┐              │
│   │               │    │                              │              │
│   │ ▸ Injection   │───▶│      🧠 ROUTER AGENT         │              │
│   │ ▸ Sanitize    │    │      Intent Classification   │              │
│   │ ▸ Length      │    │      Confidence Scoring       │              │
│   │               │    └──────────┬───────────────────┘              │
│   └──────────────┘               │                                   │
│                        ┌─────────┼─────────┬───────────┐            │
│                        ▼         ▼         ▼           ▼            │
│                    ┌───────┐ ┌───────┐ ┌───────┐ ┌──────────┐      │
│                    │  🔍   │ │  📦   │ │  ↩️   │ │   🚨     │      │
│                    │Product│ │ Order │ │Return │ │Escalation│      │
│                    │Agent  │ │ Agent │ │Agent  │ │  Agent   │      │
│                    └───┬───┘ └───┬───┘ └───┬───┘ └──────────┘      │
│                        │         │         │                         │
│                        ▼         ▼         ▼                         │
│                    ┌─────────────────────────────┐                   │
│                    │    🛠  TOOL EXECUTION        │                   │
│                    │    SQLite │ Products │ Orders │                  │
│                    └─────────────────────────────┘                   │
│                                       │                              │
│   ┌──────────────┐                    │                              │
│   │    OUTPUT     │◀───────────────────┘                              │
│   │  GUARDRAIL    │                                                   │
│   │               │                                                   │
│   │ ▸ PII Redact  │                                                   │
│   │ ▸ Policy OK   │                                                   │
│   │ ▸ No Leaks    │                                                   │
│   └──────────────┘                                                   │
│                                                                      │
│   FastAPI Backend                                                    │
└──────────────────────────────────────────────────────────────────────┘
```

<br />

## 🛡 Triple-Layer Safety

Every single message passes through **3 guardrail layers** before reaching the customer:

<table>
<tr>
<td align="center" width="33%">

**🔒 Layer 1: Input**

Prompt injection detection
12 attack pattern signatures
HTML stripping & sanitization
2,000 char limit enforcement

</td>
<td align="center" width="33%">

**🔍 Layer 2: Output**

Auto-redacts credit cards
Auto-redacts SSNs & phone numbers
Blocks false delivery promises
Catches competitor mentions

</td>
<td align="center" width="33%">

**⚖️ Layer 3: Policy**

Return window enforcement
Restocking fee calculations
VIP benefit application
Category-specific rules

</td>
</tr>
</table>

<br />

## 🧪 Try It

Drop these into the chat and watch the agents work:

<table>
<tr>
<td>💬</td>
<td><strong>"What wireless headphones do you have?"</strong></td>
<td>→ Product Specialist searches catalog, shows ratings & prices</td>
</tr>
<tr>
<td>💬</td>
<td><strong>"Compare Sony WH-1000XM5 with AirPods Pro"</strong></td>
<td>→ Side-by-side comparison with specs</td>
</tr>
<tr>
<td>💬</td>
<td><strong>"Show me my orders"</strong></td>
<td>→ Order Tracker pulls full order history</td>
</tr>
<tr>
<td>💬</td>
<td><strong>"Where is order ORD-2025-0534909?"</strong></td>
<td>→ Tracking number, carrier, estimated delivery</td>
</tr>
<tr>
<td>💬</td>
<td><strong>"I want to return the Garmin Watch from ORD-2025-0889745"</strong></td>
<td>→ Looks up order → checks eligibility → calculates refund</td>
</tr>
<tr>
<td>💬</td>
<td><strong>"I need to speak to a manager"</strong></td>
<td>→ Empathetic response + handoff summary generated</td>
</tr>
</table>

<br />

## ⚡ Quick Start

### Prerequisites
- Python 3.11+ · Node.js 18+ · [OpenAI API key](https://platform.openai.com/api-keys)

### 1. Backend

```bash
cd backend
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt

cp .env.example .env
# Add your OPENAI_API_KEY to .env

uvicorn app.main:app --reload --port 8000
# ✓ Database auto-seeds with demo data on first startup
```

### 2. Frontend

```bash
cd frontend
npm install
npm run dev
```

### 3. Open → http://localhost:3000

<br />

## 🧰 Tech Stack

<table>
<tr>
<td align="center" width="25%"><strong>🧠 AI Layer</strong></td>
<td align="center" width="25%"><strong>⚙️ Backend</strong></td>
<td align="center" width="25%"><strong>🎨 Frontend</strong></td>
<td align="center" width="25%"><strong>🗄 Data</strong></td>
</tr>
<tr>
<td>

LangGraph
LangChain
OpenAI GPT-4o
Anthropic Claude
ReAct Agents

</td>
<td>

Python 3.11
FastAPI
Pydantic
SSE Streaming
Docker

</td>
<td>

Next.js 16
React 19
TypeScript 5
Tailwind CSS 4
React Compiler

</td>
<td>

SQLAlchemy
SQLite
6 ORM Models
25 Products
1M+ Orders tested

</td>
</tr>
</table>

<br />

## 📂 Project Structure

```
agentic-customer-care/
│
├── backend/
│   └── app/
│       ├── agents/          ← 🧠 5 AI agents + LangGraph orchestrator
│       │   ├── graph.py          StateGraph wiring & routing
│       │   ├── router_agent.py   Intent classification
│       │   ├── product_agent.py  Product specialist (ReAct)
│       │   ├── order_agent.py    Order tracking (ReAct)
│       │   ├── returns_agent.py  Returns & refunds (ReAct)
│       │   └── escalation_agent.py  Human handoff
│       │
│       ├── tools/           ← 🛠 11 LangChain tools (DB-backed)
│       ├── guardrails/      ← 🛡 Input validation, output filtering, policy engine
│       ├── services/        ← 📊 Business logic (orders, products, returns)
│       ├── llm/             ← 🔌 Provider abstraction + auto-fallback
│       ├── memory/          ← 💾 Multi-turn conversation persistence
│       └── db/              ← 🗄 Models, migrations, seed data
│
├── frontend/
│   └── src/
│       ├── components/chat/ ← 💬 Chat UI, agent badges, markdown renderer
│       ├── hooks/           ← 🪝 useChat state management
│       └── lib/             ← 📡 API client, types, utilities
│
├── render.yaml              ← 🚀 One-click Render deployment
├── DEPLOYMENT.md            ← 📋 Step-by-step deployment guide
└── README.md
```

<br />

## 🔄 How Agent Reasoning Works

This isn't a simple chatbot. Each specialist uses the **ReAct (Reason + Act) pattern** — the agent thinks, decides which tool to call, observes the result, and iterates until it has a complete answer.

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  Customer: "Can I return the MacBook from ORD-2025-0335810?"   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  🧠 Think                                                │   │
│  │  "Customer wants to return a MacBook. I need to find     │   │
│  │   the order first to get the product ID."                │   │
│  └─────────────────────────────────┬───────────────────────┘   │
│                                    ▼                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  🛠 Act: lookup_order("ORD-2025-0335810")                │   │
│  └─────────────────────────────────┬───────────────────────┘   │
│                                    ▼                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  👁 Observe                                               │   │
│  │  "Delivered | MacBook Air M3 (ID:2) $1,299                │   │
│  │   + Breville Espresso Machine (ID:16) $699.95"            │   │
│  └─────────────────────────────────┬───────────────────────┘   │
│                                    ▼                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  🧠 Think                                                │   │
│  │  "MacBook = Product ID 2. Let me check eligibility."     │   │
│  └─────────────────────────────────┬───────────────────────┘   │
│                                    ▼                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  🛠 Act: check_return_eligibility("ORD-2025-0335810", 2) │   │
│  └─────────────────────────────────┬───────────────────────┘   │
│                                    ▼                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  👁 Observe                                               │   │
│  │  "ELIGIBLE | Electronics | 30-day window (18 left)        │   │
│  │   Restocking fee: 15% ($194.85) | Refund: $1,104.15"     │   │
│  └─────────────────────────────────┬───────────────────────┘   │
│                                    ▼                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  💬 Respond                                               │   │
│  │  "Your MacBook Air M3 is eligible for return! You have   │   │
│  │   18 days remaining. There's a 15% restocking fee of     │   │
│  │   $194.85, so your refund would be $1,104.15 to your     │   │
│  │   original payment method..."                             │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

<br />

## 📊 Return Policy Engine

The system enforces real business rules — not hardcoded responses:

| Category | Window | Fee | Refund To | Conditions |
|:--------:|:------:|:---:|:---------:|:----------:|
| 💻 **Electronics** | 30 days | 15% | Original payment | Original packaging + accessories |
| 👕 **Clothing** | 60 days | 0% | Original payment | Tags attached, unworn |
| 🏠 **Home & Kitchen** | 30 days | 10% | Original payment | Unused, original packaging |
| ⚽ **Sports** | 45 days | 0% | Store credit | Unused, original packaging |
| 📚 **Books** | 14 days | 0% | Original payment | No writing, undamaged |

> 👑 **VIP members** get restocking fees waived on all categories

<br />

## 📈 Stress Tested at Scale

The system has been benchmarked with **1 million orders** across 1,000 users:

```
┌────────────────────────────┬───────────┐
│ Metric                     │ Result    │
├────────────────────────────┼───────────┤
│ Single order lookup        │ < 1ms     │
│ User's orders (~1,000)     │ ~39ms     │
│ Order status check         │ < 1ms     │
│ Database size (1M orders)  │ 446 MB    │
│ Seed time (1M orders)      │ ~2 min    │
└────────────────────────────┴───────────┘
```

<br />

## 🚀 Deploy for Free

Full deployment guide: **[DEPLOYMENT.md](./DEPLOYMENT.md)**

| Service | What | Cost |
|:-------:|:----:|:----:|
| **Vercel** | Frontend (Next.js) | $0 |
| **Render** | Backend (FastAPI + Docker) | $0 |
| **OpenAI** | LLM (GPT-4o-mini) | ~$0.001/query |

```
User → Vercel (CDN + SSR)
         │
         │  /api/* proxy
         ▼
       Render (Docker)
         ├── FastAPI + LangGraph
         ├── SQLite (auto-seeded)
         └── OpenAI GPT-4o-mini
```

<br />

## 🔌 LLM Configuration

The system supports **multiple providers** with automatic fallback:

```env
# Option 1: OpenAI (Recommended)
OPENAI_API_KEY=sk-...
PRIMARY_LLM=gpt-4o-mini
FALLBACK_LLM=gpt-4o-mini

# Option 2: Anthropic
ANTHROPIC_API_KEY=sk-ant-...
PRIMARY_LLM=claude-sonnet-4-20250514

# Option 3: Both (auto-fallback)
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
# If primary fails → seamlessly switches to fallback
```

<br />

## 📡 API

```
POST /api/chat/message     Send a message, get a response
POST /api/chat/stream      Send a message, get SSE stream
GET  /api/conversations/:id List conversations
GET  /api/health            Health check
```

**Example:**
```bash
curl -X POST http://localhost:8000/api/chat/message \
  -H "Content-Type: application/json" \
  -d '{"message": "Show me my orders", "user_id": 1}'
```

<br />

---

<div align="center">

### Built with 🧠 LangGraph · ⚡ FastAPI · ⚛️ Next.js

**If you found this useful, give it a ⭐**

</div>
