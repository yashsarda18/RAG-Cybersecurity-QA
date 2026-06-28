# RAG-Cybersecurity-QA

A domain-specific Retrieval-Augmented Generation (RAG) system that generates 
actionable cybersecurity guidelines grounded in 10 authoritative NIST 
publications. Built with Mistral-7B-Instruct-v0.2 and FAISS vector search.

## 🔍 Overview
Practitioners querying cybersecurity guidelines often get hallucinated or 
generic LLM responses. This system solves that by grounding every answer 
exclusively in NIST standards — retrieving the top-3 most relevant passages 
via dense semantic search before generating structured, source-attributed 
recommendations.

## 📊 Evaluation Results (RAGAS-Aligned Metrics)
| Metric | Mean Score |
|---|---|
| Context Relevance | 0.691 |
| Answer Relevance | 0.684 |
| Faithfulness | 0.319 |

Evaluated across 10 diverse cybersecurity queries spanning incident response, 
zero trust architecture, patch management, authentication, and continuous 
monitoring.

## 🏗️ System Architecture
| Stage | Component |
|---|---|
| Document Store | 10 NIST PDFs (SP 800-61, 800-53, 800-207, CSF 2.0, +6 more) |
| Text Extraction | pdfplumber (layout-aware) |
| Chunking | Sliding window — 200 words, 30-word overlap → 2,441 clean chunks |
| Embedding Model | sentence-transformers/all-MiniLM-L6-v2 (384-dim) |
| Vector Index | FAISS IndexFlatIP (exact cosine similarity) |
| LLM | Mistral-7B-Instruct-v0.2 (4-bit NF4 quantized, ~5GB VRAM) |
| Evaluation | RAGAS-aligned proxy metrics (context relevance, answer relevance, faithfulness) |

## 📚 Knowledge Base
10 NIST publications covering:
- Incident Response (SP 800-61r2)
- Patch & Vulnerability Management (SP 800-40r4)
- Zero Trust Architecture (SP 800-207)
- Authentication & Digital Identity (SP 800-63B)
- Cybersecurity Framework (CSF 2.0)
- Email Security (SP 800-177r1)
- Access Control (SP 800-171r2)
- Security Controls (SP 800-53r5)
- Penetration Testing (SP 800-115)
- Continuous Monitoring (SP 800-137)

Total: 444,283 words → 2,441 clean retrieval chunks

## 🚀 How to Run
**Prerequisites**
```bash
pip install sentence-transformers faiss-cpu transformers accelerate 
pip install sentencepiece bitsandbytes pdfplumber pandas numpy matplotlib
```
**Setup**
1. Open `rag_cybersecurity_qa.ipynb` in Google Colab (T4 GPU recommended)
2. Run All → downloads NIST PDFs, builds FAISS index, loads Mistral-7B, 
   runs 10-query evaluation

**Note**: Requires ~5GB VRAM for 4-bit quantized Mistral-7B. 
T4 GPU (15.6GB) on Colab free tier works fine.

## 👤 Author
Yash Sarda — Master of AI & ML, Adelaide University
[LinkedIn](https://linkedin.com/in/yashsarda18) | 
[GitHub](https://github.com/yashsarda18)
