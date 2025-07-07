# 🍷 RAG Wine Recommendation Pipeline

This project implements a **Retrieval-Augmented Generation (RAG)** pipeline for personalized wine recommendations using **DeepSeek**, **Hugging Face embeddings**, and **Chroma vector store**.

---

## 🔍 Overview

This pipeline takes a user's wine preference query and returns relevant wine recommendations from a dataset using vector similarity and sommelier knowledge.

### 🔄 Core Workflow

1. **Vectorize Wines**
   - Load `wine_data.csv`
   - Generate embeddings using **local Hugging Face models** (OpenAI embeddings not usable in HK)
   - Store vectors in **ChromaDB** with cosine similarity

2. **Generate Taste Profile (optional)**
   - RAG via **DeepSeek API** + sommelier knowledge base
   - Convert generated taste description to embedding vector

3. **Similarity Search**
   - Use Chroma's `as_retriever()` to match user vector with wine vectors

4. **Recommendation Output**
   - **Option A:** Use wine tasting notes from CSV
   - **Option B:** Run another RAG step (DeepSeek + Top-K results) for refined explanation

---

## 🧪 Current Setup

- **Embeddings:** Hugging Face local models
- **RAG Model:** DeepSeek (via API calls)
- **Vector Store:** ChromaDB (cosine similarity)
- **Notebook:** `rag-env.ipynb`

---

## ⚙️ Optimization Plan

- **Speed Optimization**
  - Replace taste profile generation with **SpaCy-based NLP parser**

- **Quality Improvement**
  - **Rerank results** using:
    - Wine type relevance (e.g. red/white)
    - Price filters
    - Query-wine embedding similarity

---

## 🚀 Example Query


Wine 1: Alain Chavy  Puligny  Montrachet 202
Wine 2: Aldeneyck Herenlaak Chardonnay Maseik, Belgium 2020
WIne 3: Anne et Jean-Francois Ganevat Cotes du Jure La Barraque Savagnin 2020
Wine 4: Armand Heitz Saint Aubin 1er cru murgers dent de chien 2019
Wine 5: Billaud Simon Chablis Tete dOr 2021
> _“What wine goes well with spicy Thai green curry with coconut milk?”_

**Output:**
- Wine 1: Alain Chavy  Puligny  Montrachet 202
- Wine 2: Aldeneyck Herenlaak Chardonnay Maseik, Belgium 2020
- WIne 3: Anne et Jean-Francois Ganevat Cotes du Jure La Barraque Savagnin 2020
- Wine 4: Armand Heitz Saint Aubin 1er cru murgers dent de chien 2019
- Wine 5: Billaud Simon Chablis Tete dOr 2021

---

## 📝 Notes

- Chroma simplifies retrieval with `as_retriever()`, making it easy to swap out embedding or model sources.
- DeepSeek API used for RAG; local inference optional for future adaptation.
