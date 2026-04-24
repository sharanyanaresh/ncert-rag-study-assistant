# Reflection Report – Week 9 Mini Project

## Project Title

Retrieval-Ready Study Assistant for NCERT Science

---

## Objective

The objective of this project was to build a trustworthy AI study assistant that answers Class 9 Science questions using textbook content rather than free-form hallucinated generation.

I implemented a Retrieval-Augmented Generation (RAG) pipeline using NCERT textbook data.

---

## What I Built

I created two versions of the system:

### Version 1 – Chapter Optimized System

Focused on the chapter:

Force and Laws of Motion

This version produced highly accurate answers because retrieval search space was smaller.

### Version 2 – Full Textbook Prototype

Expanded retrieval to the entire NCERT Science textbook.

This version demonstrated scalability challenges and retrieval tuning.

---

## Technical Components Implemented

- PDF text extraction using PyMuPDF
- Text cleaning and preprocessing
- Chunking with overlap
- BM25 retrieval engine
- Groq LLM integration
- Grounded prompting
- Refusal for unknown answers
- Evaluation dataset creation

---

## Key Learnings

### 1. Retrieval Quality Determines Final Answer Quality

Even strong LLMs need relevant context.

### 2. Small Corpus vs Large Corpus Tradeoff

Single chapter retrieval was easier and more accurate than full textbook retrieval.

### 3. Hallucination Reduction Is Important

Prompting the model to answer only from context improved trustworthiness.

### 4. Real AI Engineering Requires Iteration

Many improvements came through debugging chunk size, retrieval settings, and model APIs.

---

## Challenges Faced

- PDF formatting noise
- Chapter boundary extraction
- Model API version issues
- Retrieval degradation after scaling to full textbook
- Notebook dependency order errors

---

## How I Solved Them

- Cleaned extracted text
- Used chunk overlap
- Switched to Groq API
- Added chapter-aware retrieval logic
- Re-ran notebook cells in proper order

---

## Future Improvements

- Semantic embeddings retrieval
- FAISS vector database
- Hybrid search
- Multi-language support
- Web application UI

---

## Final Reflection

This project helped me understand how real-world GenAI systems are built beyond just calling an API. I learned that data quality, retrieval logic, prompting, and evaluation are equally important. It gave me hands-on understanding of practical RAG system design.