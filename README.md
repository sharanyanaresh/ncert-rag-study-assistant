## Example Query

Question: What is Newton's second law?

Answer: Force is proportional to the rate of change of momentum and acts in the direction of applied force.

## Limitations

- Currently uses one chapter only
- BM25 lexical retrieval may miss paraphrases
- Can be extended with embeddings

# 📘 NCERT Science Retrieval-Ready Study Assistant  
### Week 9 Mini Project | Retrieval-Augmented Generation (RAG) System

A production-style mini project that builds a **trustworthy AI study assistant** for **NCERT Class 9 Science** using Retrieval-Augmented Generation (RAG).

This assistant answers questions from the textbook chapter **Force and Laws of Motion** by first retrieving relevant chapter content and then generating a grounded answer using an LLM.

If the answer is not present in the chapter context, the assistant is designed to **refuse gracefully** instead of hallucinating.

---

# 🎯 Project Objective

Build a bounded educational assistant that:

✅ Answers textbook-based questions accurately  
✅ Uses only retrieved NCERT chapter content  
✅ Reduces hallucinations using grounding prompts  
✅ Refuses out-of-scope questions  
✅ Demonstrates real-world GenAI engineering workflow

---

# 🧠 Why This Project Matters

This project simulates a real edtech product use case where trust is critical.

Example:

If a student asks:

> What is Newton’s Second Law?

The system should return the correct chapter-grounded answer.

If asked:

> What is DNA?

The system should refuse because DNA is outside the selected chapter.

---

# ⚙️ Tech Stack

| Category | Tools Used |
|--------|------------|
| Language | Python |
| Notebook | Jupyter Notebook |
| PDF Extraction | PyMuPDF |
| Data Handling | Pandas |
| Retrieval Engine | Rank-BM25 |
| Tokenizers | Hugging Face Transformers |
| LLM Provider | Groq API |
| Model Used | Llama 3.1 8B Instant |

---

# 📂 Project Structure

```text
NCERT_RAG_MINIPROJECT/
│── README.md
│── requirements.txt
│── .gitignore
│
├── data/
│   └── ncert_science_class9.pdf
│
├── notebooks/
│   └── week9_rag_project.ipynb
│
├── outputs/
│   └── evaluation_results.csv
│
├── src/
│   └── (optional modular python scripts)
│
└── venv/

📚 Dataset Used

Source: NCERT Class 9 Science Textbook

Selected Chapter:
✅ Force and Laws of Motion

Reason for selecting this chapter:

Rich conceptual content
Definitions
Newton’s Laws
Numerical examples
Real-world reasoning questions

Ideal for retrieval evaluation.

🔄 System Architecture
User Question
     ↓
BM25 Retriever
     ↓
Top Relevant Chunks
     ↓
Grounded Prompt
     ↓
Groq LLM
     ↓
Final Answer / Refusal

🧹 Pipeline Workflow
1. PDF Extraction

The full NCERT Science textbook PDF is loaded using PyMuPDF.

2. Chapter Isolation

Only pages corresponding to:

Force and Laws of Motion

were extracted.

3. Text Cleaning

Removed:

headers
page numbers
repeated footers
broken spacing
4. Tokenizer Comparison

Compared:

BERT WordPiece
GPT-2 BPE

To understand token boundaries and chunk sizing.

5. Chunking Strategy

Used:

Chunk Size = 300 words
Overlap = 50 words

This preserves continuity and avoids splitting concepts.

6. Retrieval

Implemented BM25 lexical retrieval for top-k relevant chunks.

7. Generation

Groq LLM answers only using retrieved context.

8. Guardrail Behavior

If answer not found in context:

I cannot answer from the provided chapter content.

🧪 Example Queries
In-Scope Question

Question: What is Newton's second law?

Answer: Force is proportional to the rate of change of momentum and acts in the direction of the applied force.

Out-of-Scope Question

Question: What is DNA?

Answer: I cannot answer from the provided chapter content.

📊 Evaluation Summary

Evaluation set included:

Direct textbook questions
Conceptual questions
Paraphrased questions
Out-of-scope questions

Results stored in:

outputs/evaluation_results.csv
🚀 How To Run This Project
Step 1 — Clone Repository
git clone <your-repo-link>
cd NCERT_RAG_MINIPROJECT
Step 2 — Create Virtual Environment
python -m venv venv
Step 3 — Activate Environment
Windows
venv\Scripts\activate
Step 4 — Install Dependencies
pip install -r requirements.txt
Step 5 — Add Groq API Key

Inside notebook:

client = Groq(api_key="YOUR_API_KEY")
Step 6 — Run Notebook

Open:

notebooks/week9_rag_project.ipynb

Run all cells.

📌 Key Learnings

This project demonstrates understanding of:

Retrieval-Augmented Generation (RAG)
Hallucination reduction
Grounded prompting
BM25 search systems
Chunking strategy
Tokenization impact
LLM orchestration
Honest evaluation methodology
🔮 Future Improvements

Possible production upgrades:

Dense embedding retrieval
Hybrid search (BM25 + embeddings)
Multi-chapter support
Hindi-English bilingual support
Source citations
Streamlit web interface

Author ->
Sharanya Naresh
PG Diploma AI-ML & Agentic AI Engineering
