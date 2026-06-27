# 🛒 AI-Powered Ecommerce Report Generation System

> A production-inspired prototype that automatically generates personalized **Daily Digests** and **Weekly Reports** for D2C ecommerce brands, powered by Claude AI.

---

## What Is This?

This is **not a dashboard**. This is **not a chatbot**.

It's an AI product prototype that answers one question:

> **"What changed in my business today, and should I care?"**

Running `notebook.ipynb` from top to bottom produces:

- 📊 180 days of realistic synthetic ecommerce data for 2 customer archetypes
- 🔍 Feature engineering (Z-scores, moving averages, momentum, anomaly scores)
- 🏆 A transparent, deterministic Importance Ranking Engine (0-100 score with full breakdown)
- 🎯 A 3-tier Personalization Engine (Cold Start → Warm → Mature)
- 📋 Structured JSON evidence objects (the LLM only sees what we give it)
- 🤖 AI-written Daily Digests and Weekly Reports via Claude API
- 📄 Exported Markdown + PDF reports
- 🗂️ A complete Product Design Document

---

## Quick Start

### Prerequisites
- Python 3.12+
- An Anthropic API key ([get one here](https://console.anthropic.com/))

### 1. Clone / Open the Project
```bash
cd project/
```

### 2. Create and Activate the Virtual Environment
```bash
# The venv is already created. Activate it:

# Windows (PowerShell)
.\venv\Scripts\Activate.ps1

# Windows (CMD)
venv\Scripts\activate.bat

# macOS / Linux
source venv/bin/activate
```

### 3. Set Your API Key
```bash
# Copy the example env file
copy .env.example .env   # Windows
cp .env.example .env     # macOS/Linux

# Edit .env and add your Anthropic API key
# ANTHROPIC_API_KEY=sk-ant-...
```

### 4. Launch Jupyter Notebook
```bash
jupyter notebook notebook.ipynb
```

### 5. Run All Cells
In Jupyter: **Cell → Run All**

The notebook runs end-to-end and generates all outputs automatically.

---

## Project Structure

```
project/
├── notebook.ipynb              ← Main application (run this)
├── requirements.txt            ← All dependencies
├── .env.example                ← Copy to .env and add your API key
├── .env                        ← Your local env (not committed)
│
├── generated_reports/
│   ├── daily/
│   │   ├── daily_digest_growthco_YYYYMMDD.md
│   │   ├── daily_digest_growthco_YYYYMMDD.pdf
│   │   ├── daily_digest_retailpro_YYYYMMDD.md
│   │   └── daily_digest_retailpro_YYYYMMDD.pdf
│   └── weekly/
│       ├── weekly_report_growthco_YYYYMMDD.md
│       ├── weekly_report_growthco_YYYYMMDD.pdf
│       ├── weekly_report_retailpro_YYYYMMDD.md
│       └── weekly_report_retailpro_YYYYMMDD.pdf
│
├── synthetic_data/
│   ├── ecommerce_data.csv      ← 360 rows (180d × 2 customers), 25 columns
│   └── customers.csv           ← Customer profiles
│
├── assets/
│   └── charts/                 ← PNG chart exports for PDF embedding
│
├── PRODUCT_DESIGN.md           ← Auto-generated product design document
└── README.md                   ← This file
```

---

## Two Customer Archetypes

| | **GrowthCo (A)** | **RetailPro (B)** |
|---|---|---|
| Stage | Startup | Established Brand |
| Focus | Acquisition | Operations & Retention |
| Top Metrics | Revenue, ROAS, CVR | Inventory, Returns, Fulfillment |
| Personalization Tier | Warm (45 interactions) | Mature (120 interactions) |
| Daily Revenue | ~$8k–$20k | ~$40k–$70k |
| Key Anomalies | Traffic drops, marketing spikes | Stockout events, fulfillment crisis |

---

## Synthetic Data

**180 days** of daily ecommerce metrics with:

| Metric Category | Metrics |
|---|---|
| Revenue | Revenue, Orders, Sessions, CVR, AOV |
| Paid Ads | ROAS, CAC, Spend (Meta+Google), CTR, CPM, CPC |
| Email | Email Revenue, Email Open Rate |
| Retention | Repeat Purchase Rate, Refund Rate, Checkout Abandonment |
| Operations | Inventory Units, Fulfillment SLA, Shipping Delay %, Return Rate, Support Tickets |

**Realism patterns injected:**
- 📈 Trend (linear business growth)
- 📅 Seasonality (weekly cycles, day-of-week effects, holiday spikes)
- 📉 Anomalies (traffic drops, marketing spikes, stockout events, conversion crashes)

---

## Architecture

```
Raw CSV Data
    │
    ▼
Feature Engineering          → 23 metrics × 11 derived features = 253 columns
    │
    ▼
Movement Detection           → MetricMovement objects (Z-score, severity, confidence)
    │
    ▼
Importance Ranking Engine    → 0-100 score with 6-factor breakdown (no ML)
    │
    ▼
Personalization Engine       → Customer-weighted scores (Cold/Warm/Mature)
    │
    ▼
Evidence Builder             → Structured JSON (LLM only sees this)
    │
    ▼
Claude API (Sonnet 4)        → AI-written narrative reports
    │
    ▼
Markdown + PDF Export
```

---

## Importance Ranking Formula

```
Score (0-100) =
    35% × Business Importance    (customer priority weights)
  + 25% × Statistical Surprise  (Z-score sigmoid normalized)
  + 20% × Magnitude             (absolute % change)
  + 10% × Trend Persistence     (consecutive same-direction days)
  +  5% × Novelty               (not recently seen)
  +  5% × Business Rules        (revenue/inventory safety nets)
```

Every score is fully explainable — no black box.

---

## Tech Stack

| Component | Technology |
|---|---|
| Language | Python 3.12 |
| Notebook | Jupyter |
| AI | Claude API (Anthropic) |
| Data | Pandas, NumPy, SciPy |
| Visualization | Plotly, Matplotlib |
| Statistics | Scikit-learn |
| PDF | ReportLab |
| Environment | python-dotenv |

---

## Notebook Sections

| Section | Description |
|---|---|
| 1 Introduction | System overview and architecture |
| 2 Imports | Library loading and version check |
| 3 Config | Environment, constants, directory setup |
| 4 Synthetic Data | 180-day ecommerce data generation |
| 5 Exploratory Analysis | 7 professional charts |
| 6 Customer Profiles | Two archetypes with weights and history |
| 7 Feature Engineering | 11 features per metric |
| 8 Movement Detection | MetricMovement objects with severity/confidence |
| 9 Importance Ranking | 0-100 deterministic scoring engine |
| 10 Personalization | 3-tier weight adjustment |
| 11 Evidence Builder | Structured JSON for LLM |
| 12 Prompt Engineering | System prompts, few-shot examples |
| 13 Daily Digest Generation | AI report via Claude (or fallback) |
| 14 Weekly Report Generation | AI narrative via Claude (or fallback) |
| 15 Export Reports | Markdown + PDF to `generated_reports/` |
| 16 Product Design Doc | Auto-generated `PRODUCT_DESIGN.md` |
| 17 Failure Modes | 6 failure modes with mitigations |
| 18 Evaluation | Product engagement metrics simulation |

---

## Running Without an API Key

The notebook is designed to run fully without the Claude API key.

If `ANTHROPIC_API_KEY` is not set, the notebook uses **high-quality fallback templates** for all reports. All data generation, feature engineering, ranking, personalization, evidence building, charts, and PDF exports still work.

---

## Outputs

After a full run, you'll have:

- **4 reports** (2 daily + 2 weekly) in both `.md` and `.pdf` formats
- **10 professional charts** as PNG files
- **PRODUCT_DESIGN.md** — a complete product design document
- **2 CSV datasets** — ecommerce_data.csv and customers.csv

---

## Product Design

See [PRODUCT_DESIGN.md](PRODUCT_DESIGN.md) for the full product design document covering:

- Users and Jobs-to-be-Done
- Daily vs. Weekly report strategy
- Importance ranking design
- Personalization architecture
- System architecture (Batch vs. Online, LLM placement)
- Top 6 failure modes with mitigations
- Product success metrics

---

## License

MIT — prototype use only. Not for production deployment without additional data security review.
