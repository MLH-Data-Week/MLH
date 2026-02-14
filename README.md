# Data Week Financial Analytics Application

## Overview
This application is a specialized financial analytics tool designed for 'Data Week'. It features an Agentic RAG system that extracts risk parameters from corporate Annual Reports (PDFs) and uses them to run Monte Carlo simulations on Balance Sheet Ratios.

## Architecture "Flight Plan"

The application is modularized into three main components: Agent, Engine, and UI.

### 1. Agent Layer (`app/agent/`)
This layer handles the orchestration of the LLM and RAG workflows.
- **Orchestration**: Uses **LangGraph** to manage the state and flow of the agent.
- **Tools**: Defines tools for RAG (retrieval) and data extraction.
- **State**: Manages the context passing between graph nodes.

### 2. Engine Layer (`app/engine/`)
This is the computational core of the application.
- **Simulation**: **Monte Carlo** simulations are implemented here using **Polars** for high-performance data manipulation.
- **Transforms**: Data transformation logic ensures data is in the correct format for simulation.

### 3. Database & Schemas (`app/db/` & `app/schemas/`)
- **Data Storage**: **DuckDB** is used for efficient local storage and querying of historical peer data.
- **Validation**: **Pydantic V2** schemas ensure structured data extraction from the agent.

### 4. UI Layer (`ui/`)
- **Frontend**: A **Streamlit** application provides the interactive interface for users to upload reports and view simulation results.

## Directory Structure
```
app/
├── agent/       # LangGraph nodes, state, and tools
├── api/         # FastAPI routers and endpoints
├── db/          # DuckDB connection and storage logic
├── engine/      # Monte Carlo simulator and Polars logic
└── schemas/     # Pydantic models for data validation

data/
├── extracted/   # Intermediate JSON extracts
└── raw_pdfs/    # Storage for incoming Annual Reports

ui/              # Streamlit frontend application
tests/           # Unit tests
```

## Getting Started

1.  **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

2.  **Environment Setup**:
    Copy `.env` and set your API keys.

3.  **Run the App**:
    ```bash
    streamlit run ui/app.py
    ```
