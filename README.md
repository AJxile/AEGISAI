# 🛡️ AegisAI — AI-Powered Financial Risk Guardian

AegisAI is a full-stack application that combines machine learning, a financial assistant, and a modern React dashboard to help everyday users understand financial risk in plain, beginner-friendly language.

---

## ✨ Features

- 📊 **Real-time Dashboard** — Live asset cards with prices, risk bands, momentum curves, and confidence scores
- 🕯️ **Candlestick Charts** — Real OHLC data for BTC, ETH, AAPL, TSLA, and EUR/USD
- 🤖 **Financial Assistant** — Answers common questions using the latest stored market and risk data
- 🧠 **Machine Learning Pipeline** — Isolation Forest (anomaly detection) + Logistic Regression (risk classification)
- 💬 **Natural Language Understanding** — Recognizes aliases like "Bitcoin" → BTC-USD, "Apple" → AAPL
- 🔒 **Local-first Runtime** — Databases, account data, and generated files stay on the user's computer

---

## 🗂️ Repository Structure

```
AEGISAI/
├── main.py                → Unified FastAPI app with all endpoints
├── finance_assistant.py   → Data-grounded financial assistant
├── database.py            → SQLite schema definition
├── data_collector.py      → Yahoo Finance data fetcher
├── feature_engineering.py → Financial feature calculation
├── train.py               → ML model training
├── ml_models.py           → Model loading and prediction
├── risk_engine.py         → Runs predictions and stores results
├── db_tools.py            → Database helper class
├── config.py              → Centralized configuration
├── schemas.py             → API request/response models
├── run_local.py           → Local backend startup
├── forecasting/           → Forecasting models and utilities
├── routes/                → FastAPI route modules
├── services/              → Background update and notification services
└── AegisAI_Website/       → React + TypeScript + Vite frontend
    ├── src/
    ├── public/
    └── package.json
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | FastAPI (Python) |
| Database | SQLite + SQLAlchemy |
| Machine Learning | scikit-learn |
| Data Source | Yahoo Finance (yfinance) |
| Frontend | React + TypeScript + Vite |
| Styling | Tailwind CSS |
| API Server | Uvicorn |

---

## 🚀 Local Setup

### Prerequisites
- Python 3.10+
- Node.js 18+

### Windows quick start

```bash
# 1. Clone the repository
git clone https://github.com/AJxile/AEGISAI.git
cd AEGISAI

# 2. Create a virtual environment and install the backend
py -m venv .venv
.\.venv\Scripts\Activate.ps1
py -m pip install -r requirements.txt

# 3. Install the frontend and start the complete app
cd AegisAI_Website
npm ci
npm run dev
```

`npm run dev` starts both the FastAPI backend and the Vite frontend on Windows. Open **http://localhost:8000** in your browser.

### macOS and Linux

Run the backend and frontend in separate terminals after cloning the repository.

```bash
# Terminal 1: backend
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python run_local.py

# Terminal 2: frontend
cd AegisAI_Website
npm ci
npm start
```

Open **http://localhost:8000** in your browser. The backend API runs at **http://127.0.0.1:8010**.

> ⚠️ Both backend and frontend must be running at the same time.

The SQLite database is created locally. On startup, the backend also starts its market-data update in the background, so the first results may take a moment to appear.

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Health check |
| GET | `/health` | Service status |
| POST | `/chat` | AI chatbot |
| GET | `/get-data` | Raw market data |
| GET | `/risk/latest` | Latest risk prediction |
| GET | `/risk/history` | Historical risk data |
| GET | `/risk/all` | Risk for all symbols |
| GET | `/dashboard/assets` | Asset cards data |
| GET | `/dashboard/candles` | Candlestick chart data |
| GET | `/graph/price` | Price chart (PNG) |
| GET | `/graph/risk` | Risk chart (PNG) |

Interactive API docs available at: **http://127.0.0.1:8010/docs**

---

## 🧠 Machine Learning Pipeline

```
data_collector.py       → Fetch 365 days of OHLCV data from Yahoo Finance
      ↓
feature_engineering.py  → Calculate daily returns, 7d volatility, MA7, MA30
      ↓
train.py                → Train Isolation Forest + Logistic Regression → save .pkl
      ↓
risk_engine.py          → Run predictions → store in market_risk_predictions table
      ↓
main.py / chatbot       → Serve results via API and AI explanations
```

### Models
- **Isolation Forest** → Anomaly detection (1=normal, -1=anomaly)
- **Logistic Regression** → Risk classification (0=LOW, 1=HIGH)

---

## 💬 Chatbot Examples

```
"Is Bitcoin safe right now?"
"What is the risk for AAPL?"
"Compare ETH and BTC"
"Show me the trend for Tesla over the last 7 days"
"What is volatility?"
```

The chatbot recognizes common names:
- Bitcoin / BTC → BTC-USD
- Ethereum / ETH → ETH-USD
- Apple → AAPL
- Tesla → TSLA
- Euro / EUR → EURUSD=X

---

## 📈 Supported Assets

| Symbol | Name | Category |
|--------|------|----------|
| BTC-USD | Bitcoin | Cryptocurrency |
| ETH-USD | Ethereum | Cryptocurrency |
| AAPL | Apple Inc. | Stock |
| TSLA | Tesla Inc. | Stock |
| EURUSD=X | EUR/USD | Forex |

---

## 🔐 Security

- Environment files, local databases, account data, caches, and installed dependencies are excluded by `.gitignore`
- Generated runtime data stays on each user's computer

---

## 🗺️ Roadmap

- [ ] Portfolio simulation (input your own holdings)
- [ ] Explainable AI with bullet points and percentages
- [ ] Real-time price updates
- [ ] Mobile-responsive improvements

---

## 👩‍💻 Authors

- **Tesnim** — Backend, ML pipeline, AI chatbot
- **Anas** — Backend , Frontend
- **Islem**_Frontend design and React components

---

## 📄 License

This project was developed as an academic project at **Université Internationale de Tunis (UIT)** — Software Engineering Department.

> ⚠️ **Disclaimer:** AegisAI is an educational project. All outputs are for informational purposes only and do not constitute financial advice.
