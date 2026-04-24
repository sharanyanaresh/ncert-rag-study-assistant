# Reflection Questionnaire – Week 9 Mini Project

## Part A — Your implementation artifacts

### A1. Your chunking parameters

For the primary chapter-focused system, I used:

- Chunk size: 300 words  
- Overlap: 50 words  
- Chunking method: fixed-size word chunks with overlap

For the full textbook prototype, I later tested:

- Chunk size: 180 words  
- Overlap: 40 words

The observation that pushed me to choose 300/50 for the chapter version was that smaller chunks (around 150–200 words) often split a definition from its explanation or example. Larger chunks preserved concept continuity and helped retrieval for questions like “What is Newton’s second law?” The 50-word overlap helped avoid losing information at chunk boundaries.

---

### A2. A retrieved chunk that was wrong for its query

Query:

> What is photosynthesis?

Wrong retrieved chunk:

> Motion of objects along a straight line can be represented using distance-time graphs and velocity-time graphs...

The retriever returned this because the full textbook corpus became much larger, and BM25 lexical retrieval was matching common words while failing to prioritize semantically correct biology chunks. The issue was not only retrieval quality but also noisy PDF extraction and weak lexical ranking across multiple chapters.

---

### A3. Your grounding prompt, v1 and v(final)

#### Prompt v1

```text
Answer only from the context below.
Context: {context}
Question: {question}
Answer:This version sometimes still produced guesses when context was weak.

Prompt (final)
You are an NCERT Class 9 Science study assistant.

Use ONLY the context below to answer the question.

If the answer is not clearly available in the context, reply exactly:

I cannot answer from the provided textbook content.

Context:
{context}

Question:
{question}

Answer:
The revision was caused by observing failures on out-of-scope questions like “What is DNA?” during the chapter-only version. The first prompt encouraged preference for context, but not strict refusal. The final prompt reduced hallucinations significantly.

Part B — Numbers from your evaluation
B1. Your evaluation scores

Out of 15 questions:

Correct: 13
Grounded: 13
Appropriate refusals: 2

The number that bothered me most was groundedness. Even when answers looked correct, I learned that correctness alone is not enough for a trustworthy system. If the answer is not supported by retrieved chunks, it is risky in an educational setting.

B2. If you ran the chunk-size experiment

Yes.

Compared:

300 words + 50 overlap
180 words + 40 overlap

Observed result:

Smaller chunks slightly improved topic precision in the full textbook setup.
Larger chunks worked better for the single chapter setup.
Refusal behavior did not change much because that depended more on prompting than chunk size.
B3. If you compared model families

I compared:

Groq Llama 3.1 8B Instant
BM25 retrieval only (no generation layer, just chunk inspection)

The Groq model performed better for explanatory answers. Retrieval-only outputs were useful for debugging but not student-friendly.

Specific question:

What is Newton’s second law?

Retrieval only:

Force is proportional to rate of change of momentum...

Groq answer:

Newton’s second law states that the rate of change of momentum of an object is proportional to the applied unbalanced force and occurs in the direction of the force.

Part C — Debugging moments
C1. The most frustrating bug

The most frustrating bug was repeated API/model errors while integrating generation. I first tried Gemini, but model/version mismatches and API issues slowed progress. Then I switched to Groq and initially used a retired model name.

It took around 2–3 hours total across attempts.

The actual fix was switching to a supported Groq model:

llama-3.1-8b-instant

If someone hits this bug next week, the fastest solution is to test API connectivity first, then verify the exact current model name from provider documentation.

C2. What still bothers you

The full textbook version still bothers me because retrieval quality dropped compared to the chapter-specific version. Questions like “What is photosynthesis?” should work, but lexical retrieval over a large noisy corpus was inconsistent.

To fix this properly, I would implement semantic embeddings retrieval (SentenceTransformers + FAISS) or hybrid BM25 + vector search.

Part D — Architecture and reasoning
D1. Why not just ChatGPT?

A generic chatbot can answer many science questions, but it may answer from general internet knowledge rather than NCERT textbook wording. In this project, the chapter-specific RAG system correctly refused questions like “What is DNA?” when DNA was outside the selected chapter. That refusal behavior is valuable because it preserves trust and scope control.

For an education company, textbook alignment matters more than generic fluency.

D2. The GANs reflection

GANs are designed mainly for generating realistic synthetic data such as images, audio, or similar content through competition between generator and discriminator models. That is not the core requirement here.

This project needs retrieval, grounding, and factual answering from trusted source text. GANs do not naturally solve document retrieval or evidence-grounded QA.

The deeper principle is that architectures must match the problem. Using an impressive model type is less important than choosing the right system design for the task.

D3. Honest pilot readiness

My honest answer is: not yet for 100 students next Monday.

The chapter-specific version is strong enough for a controlled demo, but the full textbook version still needs retrieval improvements.

Three things I would verify first:

Improve multi-chapter retrieval quality using embeddings or hybrid search
Expand evaluation set using real student-style messy queries
Add citations/page references so answers are auditable
Part E — Effort and self-assessment
E1. Effort rating

I would rate my effort as 9/10.

One thing I am genuinely proud of is that I did not stop after making the chapter version work. I also attempted to scale it to the full textbook and learned where the real challenges begin.

E2. The gap between you and a stronger student

A stronger student may have implemented dense retrieval (FAISS + embeddings) and compared it against BM25.

I did not complete that mainly due to time and because I prioritized finishing a reliable end-to-end system first.

E3. What would change with two more days

The first thing I would do is replace BM25 full-textbook retrieval with semantic vector retrieval.

The last thing I would do is build a simple Streamlit interface so students can interact with the assistant in a polished product format.