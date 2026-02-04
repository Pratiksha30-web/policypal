# 📄 RAG-Based Google Doc Chatbot (Gemini + FAISS + Sentence Transformers)

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://policypalassignment-koaszomdwha3zn6kyedziu.streamlit.app/)

A full-stack **Retrieval-Augmented Generation (RAG)** chatbot that automatically ingests content from a publicly shared Google Document and answers user queries with **accurate, citation-grounded responses**.

The system uses **Sentence Transformers for embeddings**, **FAISS for vector search**, and **Google Gemini SDK** for answer generation. It includes a **FastAPI backend**, **Streamlit demo app**, and **HTML/CSS/JS frontend UI**.

---

## 🚀 Features

- ✅ Automatic Google Doc ingestion
- ✅ Structured section-aware parsing
- ✅ Semantic chunking with overlap
- ✅ Dense embeddings using Sentence Transformers
- ✅ Fast similarity search using FAISS
- ✅ Gemini-powered grounded answer generation
- ✅ Inline source citations
- ✅ FastAPI backend API
- ✅ Streamlit deployed demo app
- ✅ Web-based frontend UI
- ✅ Config-driven modular pipeline
- ✅ Production-ready architecture

---

## 🏗 System Architecture

```
Public Google Doc
        ↓
Ingestion Layer
        ↓
Structured Parsing
        ↓
Semantic Chunking
        ↓
Sentence Transformer Embeddings
        ↓
FAISS Vector Index
        ↓
Query Embedding
        ↓
Similarity Search
        ↓
Gemini RAG Generation
        ↓
FastAPI Backend
        ↓
Frontend UI / Streamlit App
```

---

## 📂 Project Structure

```
rag-chatbot/
│
├── config/
│   └── config.yaml
│
├── ingestion/
│   ├── fetch_doc.py
│   ├── normalize.py
│   └── run_ingestion.py
│
├── chunking/
│   ├── semantic_chunker.py
│   └── run_chunking.py
│
├── embeddings/
│   ├── embedder.py
│   ├── vector_store.py
│   └── run_embedding.py
│
├── retrieval/
│   └── retriever.py
│
├── rag/
│   └── rag_pipeline.py
│
├── ui/
│   ├── frontend/
│   │   ├── index.html
│   │   ├── style.css
│   │   └── app.js
│   │
│   ├── backend/
│   │   └── app.py   (FastAPI)
│   │
│   └── streamlit_app.py
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── vector_db/
│
├── .env
├── requirements.txt
└── README.md
```

---

## ⚙ Tech Stack

| Component             | Technology                                |
| --------------------- | ----------------------------------------- |
| LLM                   | Google Gemini (google-genai SDK)          |
| Embeddings            | Sentence Transformers (all-MiniLM-L6-v2)  |
| Vector Database       | FAISS                                     |
| Backend API           | FastAPI                                   |
| Frontend              | HTML, CSS, JavaScript                     |
| Demo App              | Streamlit (Deployed)                      |
| Config                | YAML                                      |
| Environment Variables | python-dotenv                             |
| Hosting               | Streamlit Cloud (Live) / Render (Planned) |

---

## 🌐 Live Demo

**Streamlit App:**  
👉 https://policypalassignment-koaszomdwha3zn6kyedziu.streamlit.app/

---

## 🚦 Deployment Status

- Streamlit Demo: ✅ Live
- FastAPI Backend: 🚧 In Progress
- Production Frontend UI: 🚧 In Progress

---

## 🔑 Prerequisites

- Python 3.9+
- Google Gemini API Key
- Public Google Document Link

---

## 🔧 Installation

### 1️⃣ Clone Repository

```bash
git clone https://github.com/yourusername/rag-chatbot.git
cd rag-chatbot
```

---

### 2️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

---

### 3️⃣ Environment Setup

Create `.env` file:

```env
GEMINI_API_KEY=your_api_key_here
```

---

### 4️⃣ Configuration

Edit `config/config.yaml`

```yaml
google_doc_url: "PASTE_PUBLIC_GOOGLE_DOC_LINK"

embedding:
  model_name: all-MiniLM-L6-v2

retrieval:
  top_k: 3

gemini:
  model_name: gemini-2.5-flash
  temperature: 0.2
  max_output_tokens: 1024
```

---

## ▶ Pipeline Execution

### ✅ Step 1 — Document Ingestion

```bash
python -m ingestion.run_ingestion
```

---

### ✅ Step 2 — Semantic Chunking

```bash
python -m  chunking.run_chunking
```

---

### ✅ Step 3 — Embedding + Index Creation

```bash
python embeddings/run_embedding.py
```

---

### ✅ Step 4 — Run Streamlit App

```bash
streamlit run ui/streamlit_app.py
```

---

## 🚀 Running FastAPI Backend

### Start API Server

```bash
uvicorn app:app --reload
```

---

### API Base URL

```
http://127.0.0.1:8000
```

---

### Swagger API Docs

```
http://127.0.0.1:8000/docs
```

---

### Example API Request

```json
{
  "query": "What is the leave policy?",
  "chat_history": []
}
```

## 🐳 Quick Start with Docker Hub

You can run the PolicyPal backend directly from the pre-built image hosted on Docker Hub.

### 1. Pull and Run the Image

Replace YOUR_API_KEY with your Gemini API Key:

```
docker run -d -p 8000:8000 -e GEMINI_API_KEY="AIzaSyDfL4hqY3oTRKugGn7XHUUAZY1_jNO2rcQ" --name policypal-app bazy07/policy-pal-api:v1

```

### 2. Initialize the Knowledge Base

Since the vector database starts empty, run the following command to ingest the policy documents from the Google Doc into the running container:

```
docker exec -it policypal-app sh -c "python -m ingestion.run_ingestion && python -m chunking.run_chunking && python embeddings/run_embedding.py"
```

### 3. Access the API

```
Backend API: http://localhost:8000
```

### Example API Response

```json
{
  "answer": "Employees are entitled to 12 casual leaves per year.",
  "sources": [
    {
      "section_id": "3.2",
      "title": "Leave Policy",
      "chunk_id": "chunk_14"
    }
  ],
  "timestamp": "2026-01-17T10:12:44"
}
```

---

## ✅ Project Highlights

- End-to-end RAG pipeline implementation
- Google Doc live ingestion system
- Modular scalable architecture
- Production-style backend + frontend separation
- Industry-standard FAISS vector search
- Citation grounded responses

---

## 📌 Author

**Pratiksha Kumari**  
AI/ML | Data Science | RAG Systems | NLP Applications

---
