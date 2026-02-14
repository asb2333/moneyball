# Moneyball

> **Kaggle 5-Day Agents Capstone Project**  
> **Track**: Enterprise Agents  

Production-ready multi-agent stock prediction system using Google's Agent Development Kit (ADK) and A2A Protocol v0.3.0

[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![ADK](https://img.shields.io/badge/Google-ADK-4285F4)](https://google.github.io/adk-docs/)
[![A2A Protocol](https://img.shields.io/badge/Protocol-A2A%20v0.3.0-green)](https://a2a-protocol.org/)

---

## 🎯 Project Overview

A **production-grade multi-agent system** that analyzes stocks using **6 specialized AI agents** communicating via the **Agent-to-Agent (A2A) protocol**. Each agent is an expert in their domain, and a central orchestrator synthesizes their insights into actionable predictions with investor-friendly explanations.

**🔗 Repository**: [https://github.com/nishapp/agents-5days-kaggle-competition](https://github.com/nishapp/agents-5days-kaggle-competition)

### 🏆 Key Features
- ✅ **Full A2A Protocol v0.3.0** with JSONRPC transport
- ✅ **4 Real Financial APIs** (Polygon.io, FRED, NewsAPI, SEC Edgar)
- ✅ **6 Specialized Agents** working in parallel
- ✅ **4-10 second** end-to-end analysis time
- ✅ **Modern Next.js Frontend** with real-time visualization
- ✅ **Production Deployment** on Google Cloud Run
- ✅ **Comprehensive Jupyter notebook** demonstration

## 🚀 Quick Start

### ☁️ Deploy to Google Cloud (Recommended)

Get your system live in production in 15 minutes:

```bash
# One-command deployment
./deploy/deploy.sh && ./deploy/deploy-vertex-ui.sh
```

See **[VERTEX_AI_DEPLOYMENT.md](VERTEX_AI_DEPLOYMENT.md)** for complete instructions.

### 💻 Run Locally

**Prerequisites:**
- Python 3.11 or higher
- Node.js 18+ (for frontend)
- API Keys (see below)

**Installation:**

```bash
# 1. Clone repository
git clone https://github.com/nishapp/agents-5days-kaggle-competition.git
cd agents-5days-kaggle-competition

# 2. Create virtual environment
python3.11 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install Python dependencies
pip install -r requirements.txt

# 4. Install frontend dependencies
cd frontend
npm install
cd ..

# 5. Configure API keys
cp .env.example .env
# Edit .env and add your keys (see API Keys section below)
```

**Running the System:**

```bash
# Start all services
bash scripts/start_full_system.sh

# Access the frontend at http://localhost:3001
# Backend API runs on http://localhost:8000
```

**Jupyter Notebook:**

```bash
# Launch Jupyter
jupyter notebook

# Open: notebooks/kaggle_submission_complete.ipynb
```

---

## 🔑 API Keys Setup

### Required Keys

#### 1. **GOOGLE_API_KEY** (Required)
- **Purpose:** Powers all 6 AI agents using Gemini models
- **Get it:** https://aistudio.google.com/apikey
- **Cost:** Free tier available

#### 2. **POLYGON_API_KEY** (Required)
- **Purpose:** Stock prices, fundamentals, technicals, and news
- **Get it:** https://polygon.io/dashboard/api-keys
- **Cost:** Paid subscription required

### Optional Keys

#### 3. **FRED_API_KEY** (Recommended)
- **Purpose:** Macro-economic data (GDP, inflation, Fed rates)
- **Get it:** https://fred.stlouisfed.org/docs/api/api_key.html
- **Cost:** FREE

#### 4. **NEWS_API_KEY** (Optional)
- **Purpose:** Alternative news source (Polygon already provides news)
- **Get it:** https://newsapi.org/register
- **Cost:** Free tier = 100 requests/day

### Configuration

Edit `.env` file:
```bash
GOOGLE_API_KEY=your_google_api_key_here
POLYGON_API_KEY=your_polygon_api_key_here
FRED_API_KEY=your_fred_api_key_here  # Optional but recommended
NEWS_API_KEY=your_news_api_key_here  # Optional
```

---

## 📁 Project Structure

```
agents-5days-kaggle-competition/
├── agents/                      # A2A Agent Servers
│   ├── fundamental_analyst_server.py
│   ├── technical_analyst_server.py
│   ├── news_sentiment_analyst_server.py
│   ├── macro_analyst_server.py
│   ├── regulatory_analyst_server.py
│   ├── predictor_agent_server.py
│   └── kaggle_orchestrator.py   # Main orchestrator
├── tools/                       # Data fetching tools
│   ├── polygon_fetcher.py       # Stock data from Polygon
│   ├── fred_fetcher.py          # Macro data from FRED
│   ├── news_fetcher.py          # News from multiple sources
│   └── sec_edgar_fetcher.py     # SEC filings
├── frontend/                    # Next.js Frontend
│   ├── app/
│   │   ├── page.tsx            # Main dashboard
│   │   ├── components/         # React components
│   │   └── api/                # API routes
│   └── package.json
├── notebooks/                   # Jupyter notebooks
│   └── kaggle_submission_complete.ipynb  # Full demo
├── deploy/                     # GCP deployment files
├── scripts/                    # Utility scripts
├── main.py                     # CLI entry point
├── frontend_api.py             # Backend API wrapper
├── requirements.txt            # Python dependencies
└── README.md                   # This file
```

---

## 📊 Sample Analysis Output

```
🔍 Analyzing AAPL for next_quarter...
============================================================
📊 Phase 1: Specialist Agent Analysis
------------------------------------------------------------
   🔄 Calling Fundamental Analyst...
   🔄 Calling Technical Analyst...
   🔄 Calling Sentiment Analyst...
   🔄 Calling Macro Analyst...
   🔄 Calling Regulatory Analyst...

   🟢 Fundamental: Signal +0.40, Confidence 78%
   🟢 Technical: Signal +0.24, Confidence 57%
   🟢 Sentiment: Signal +0.47, Confidence 65%
   🟡 Macro: Signal +0.30, Confidence 72%
   🟡 Regulatory: Signal +0.00, Confidence 58%

🎯 Phase 2: Final Prediction Synthesis
------------------------------------------------------------
   📊 Final Recommendation: BUY
   💪 Confidence: 66.0%
   ⚡ Risk Level: MEDIUM
   ⏱️  Completed in 4.18s
```

---

## 🧪 Testing

### Verify Setup
```bash
python verify_setup.py
```

### Test Individual Agent
```bash
# Start agents
bash scripts/start_all_agents.sh

# Test fundamental agent
curl http://localhost:8001/.well-known/agent-card.json

# Expected: JSON with agent metadata
```

### Run Full Analysis
```bash
python main.py --ticker AAPL
```

---

## 📚 Documentation

- **[VERTEX_AI_DEPLOYMENT.md](VERTEX_AI_DEPLOYMENT.md)** - Complete cloud deployment guide
- **notebooks/kaggle_submission_complete.ipynb** - Full demonstration with live analysis

