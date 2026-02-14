# [Project Name]: The Corporate "Flight Simulator"

### **"Predicting the Crash Before the Storm"**
**Data Week 2026** | A Multi-Agent System for Financial Risk Quantization

---

## ⚡ ELI5: How it Works
**Think of this project like a professional Flight Simulator for a multi-billion dollar corporation.**

1.  **The Inputs (The Weather & The Plane):** We feed the system the company's **Financial Statements** (the "Plane's" current status) and the "Weather Forecast"—consisting of the **Annual Information Form (AIF)** and the Bank of Canada's **Monetary Policy Report (MPR)**.
2.  **The Agent (The Pilot):** An AI agent built with **LangGraph** "reads" the reports. If it sees a storm coming—like the Bank of Canada warning about persistent inflation or the AIF mentioning supply chain fragility—it translates that sentiment into a numerical "shock."
3.  **The Simulation (The Flight):** We don't just fly the plane once. We fly it **10,000 times** using a **Monte Carlo simulation**. Each time, the wind and rain are slightly different based on the AI pilot's findings.
4.  **The Output (The Survival Score):** The system provides a **Survival Probability**. If the plane "crashes" (liquidity runs dry) in 4,000 out of 10,000 flights, the system flags a high risk of a financial crunch.

---

## 🧠 System Logic & Optimization



### **1. Inputs (The Raw Materials)**
* **Unstructured Data:** Canadian **Annual Information Forms (AIF)**, MD&A filings (SEDAR+), and Bank of Canada **Monetary Policy Reports (MPR)**.
* **Structured Data:** Historical Balance Sheet ratios (Current Ratio, Debt-to-Equity) stored in **DuckDB**.
* **User Shocks:** Manual "What-If" overrides (e.g., "Simulate a 2% surprise interest rate hike by the BoC").

### **2. The Methodology: Qualitative to Quantitative**
We bridge the gap between "Fuzzy" human language and "Hard" statistical probability:
* **Semantic Extraction:** We use **LangChain** to pinpoint liquidity-specific risks in 200+ page AIF documents.
* **Pydantic Mapping:** An LLM extracts risks into a strict schema, converting a phrase like *"We anticipate a decline in credit availability"* into a `-0.05` mean-shift for the simulation.
* **Stochastic Modeling:** We run 10,000 parallel futures using **Polars**. We apply 'Random Walks' to the historical data, weighted by the AI's extracted risk sentiment.

### **3. The Optimization Goal**
We optimize for **Capital Resilience**. The system identifies the "Optimal Ratio Corridor"—the sweet spot where a company has enough cash to survive a 95th-percentile "storm" without leaving too much capital idle and unproductive.

---

## 🏗️ Architecture "Flight Plan"



### **1. Agent Layer (`app/agent/`)**
The "Brain" of the system.
* **LangGraph Orchestration:** Manages the stateful loop of "Read -> Extract -> Validate."
* **Agentic Tools:** Custom tools for PDF retrieval and semantic extraction from SEDAR+ style documents.

### **2. Engine Layer (`app/engine/`)**
The "Physics" of the simulator.
* **Vectorized Simulation:** Uses **Polars** and **NumPy** for high-speed, parallel Monte Carlo trials.
* **Risk Logic:** Translates Pydantic objects into mathematical shocks (e.g., Volatility Stretching).

### **3. Data & UI (`app/db/` & `ui/`)**
* **Storage:** **DuckDB** manages peer benchmarking and historical TSX data.
* **Interface:** **Streamlit** provides an interactive dashboard with probability histograms.

---

## 📂 Directory Structure
```text
app/
├── agent/       # LangGraph orchestration and AI Tools
├── db/          # DuckDB connection & Historical Data
├── engine/      # Vectorized Monte Carlo logic (Polars/Numpy)
├── schemas/     # Pydantic V2 models (The "Security Guard")
└── api/         # FastAPI endpoints (Async)
ui/              # Streamlit Frontend
data/            # raw_pdfs/ (AIFs/MPRs) and processed_json/
```
# 🚀 The "Edge"
Why this wins: Unlike a typical chatbot, [Project Name] never lets the AI do the math. The LLM acts strictly as a Parameter Extractor, translating human sentiment into statistical parameters, while our Pure Python Engine handles the rigorous computation. This eliminates hallucinations and ensures 100% calculation accuracy—crucial for high-stakes financial decisions.

# 🛠️ Getting Started
Install Dependencies:

```Bash
pip install -r requirements.txt
```

Environment Setup:
Create a .env file in the root directory and add your API keys:

`
OPENAI_API_KEY=your_key_here
TAVILY_API_KEY=your_key_here
DATABASE_URL=duckdb:///app/db/financials.db
`

Run the Application:

```Bash
streamlit run ui/app.py
```
# 📊 Roadmap & Future Enhancements
- [ ] Multi-Ticker Benchmarking: Compare "Survival Scores" across an entire TSX sector in real-time.

- [ ] Live News Feed Integration: Use Tavily to ingest breaking news from the Financial Post or Globe and Mail.

- [ ] Sensitivity Heatmaps: Visualizing which specific macro variable (BoC Rates vs. CAD/USD exchange) is the "Primary Engine Failure" point.