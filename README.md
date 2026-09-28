# BIS Certification Agent

A standalone module of a larger Agentic RAG system designed to assist with Bureau of Indian Standards (BIS) certification processes, guidelines, documentation, and compliance queries.

---

## Planned Pipeline

```
Official BIS HTML/PDF
         ↓
  Text Extraction
         ↓
     Cleaning
         ↓
     Metadata
         ↓
     Chunking
         ↓
    Embeddings
         ↓
Qdrant Vector Database
         ↓
 Certification Agent
```

---

## Project Structure

```
bis-certification-agent/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── ingestion/
│
├── agent/
│
├── config.py
├── main.py
├── requirements.txt
├── .env
├── .gitignore
└── README.md
```

### Directory & File Overview

* **`data/raw/`**:
  Stores original BIS HTML pages and PDF documents collected directly from official BIS sources. Original source files remain untouched and immutable.

* **`data/processed/`**:
  Stores intermediate and processed data assets, including extracted text, cleaned text, chunked JSON documents, and embedding-related metadata.

* **`ingestion/`**:
  Contains data collection scripts (e.g., `1_collect_bis_sources.py`) to acquire and preserve official BIS sources. Future pipeline stages will add text extraction, cleaning, chunking, and vector indexing scripts.

* **`agent/`**:
  Dedicated module for the future LangGraph Certification Agent: agent workflows, state management, system prompts, decision nodes, and retrieval tools.

* **`config.py`**:
  Central configuration hub managing filesystem paths, environment variables loaded via `.env`, and placeholders for future model and Qdrant settings.

* **`main.py`**:
  Minimal entry point placeholder verifying project initialization. FastAPI endpoints and agent execution logic will be added here in upcoming phases.

* **`requirements.txt`**:
  Pinned minimal dependencies required for the project foundation and future data ingestion tasks.

* **`.env`**:
  Environment configuration template for sensitive credentials, database hosts, and API keys.

* **`.gitignore`**:
  Configured for Python development, ensuring virtual environments, build artifacts, temporary files, data files, and `.env` remain untracked.

---

## Getting Started

### 1. Prerequisites
- Python 3.10 or higher

### 2. Environment Setup

Create and activate a virtual environment:

```bash
# Windows
python -m venv venv
.\venv\Scripts\activate

# Linux/macOS
python3 -m venv venv
source venv/bin/activate
```

Install minimal foundational dependencies:

```bash
pip install -r requirements.txt
```

### 3. Configuration
Copy or edit `.env` with your local settings (placeholders provided by default):

```bash
# Verify .env settings
cat .env
```

### 4. Verification
Run the placeholder entry point:

```bash
python main.py
```

---

## BIS Certification MCP Integration

The BIS Certification Agent is integrated with 5 standardized Model Context Protocol (MCP) retrieval tools:

```
Certification Agent
       ↓
MCP Retrieval Tools
       ↓
  Dual Retrieval
       ↓
    Qdrant
       ↓
BIS Knowledge Base
```

### Key Highlights:
- **Standardized Tools**: Exposes 5 dedicated MCP retrieval tools: `search_certification`, `get_scheme_information`, `get_license_information`, `get_certification_fees`, and `get_qco_information`.
- **Direct Dual Retrieval**: MCP tools interact directly with underlying dual retrieval capabilities without subprocess client/server transport overhead.
- **Preserved Core Pipelines**: MCP retrieval tools do **NOT** replace or bypass:
  - MiniLM embeddings (`sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2`, 384-d)
  - Cosine similarity vector search
  - Qdrant vector database (`bis_certification` & `bis_certification_expansion`)
  - Dual retrieval merging & reranking (`agent/dual_retrieval.py`)
  - Context assembly (`agent/context_builder.py`)
  - Gemini LLM answer generation (`agent/answer_generator.py`)
  - LangGraph state graph workflow (`agent/langgraph_certification.py`)

"# BIS-CertificationAgent" 
