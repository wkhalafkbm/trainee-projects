# Project 1: Document Q&A with RAG

**Stack:** watsonx.ai  
**Duration:** 1 week  
**Difficulty:** Tier 1 — Foundation

---

## Overview

Build an assistant that can answer questions about a set of documents. A user uploads or points to documents (PDFs, text files), and the assistant retrieves relevant content from them to answer questions accurately — without hallucinating information that isn't there.

This is one of the most common real-world AI use cases, and it introduces the two most important concepts a developer needs to understand before building anything more complex: how to prompt a model effectively, and how to ground it in real data.

---

## What to Build

A working RAG (Retrieval-Augmented Generation) pipeline with:

1. **Document ingestion** — load and chunk documents into a vector store
2. **Retrieval** — given a user question, find the most relevant chunks
3. **Generation** — pass retrieved chunks to a watsonx.ai model with a well-crafted prompt to produce a grounded answer
4. **A simple interface** — a minimal UI or CLI where a user can ask questions and see answers

The domain of the documents is up to the trainee, but a good default is a set of company policy documents, a product manual, or a few publicly available reports.

---

## Week Plan

### Day 1 — Understand the problem
- Read about RAG architecture: what a vector store is, what embeddings are, why chunking matters
- Set up the watsonx.ai environment and confirm API access
- Choose a document set (3–5 documents is enough to start)

### Day 2 — Build the ingestion pipeline
- Load documents and split them into chunks
- Generate embeddings using watsonx.ai embedding models
- Store embeddings in a vector store (Chroma, FAISS, or watsonx's built-in options)
- Deliverable: a script that ingests documents and stores them

### Day 3 — Build the retrieval + generation pipeline
- Given a user query, retrieve the top-k relevant chunks
- Construct a prompt that includes the retrieved context and the question
- Call a watsonx.ai foundation model and return the answer
- Deliverable: an end-to-end pipeline that answers a question from documents

### Day 4 — Improve and iterate
- Experiment with chunk size and overlap — how does it affect answer quality?
- Try different prompt structures — when does the model perform better?
- Add a "source" citation to every answer (which document and section it came from)
- Deliverable: at least 3 documented prompt/chunking experiments with observations

### Day 5 — Evaluate and break it
- Build a test set of at least 20 questions with expected answers
- Score the system: how many does it get right, partially right, or wrong?
- Find at least 3 questions the system answers incorrectly — diagnose why
- Attempt at least one fix and show whether it improved the score
- Deliverable: evaluation report (can be a simple markdown file or spreadsheet)

---

## Key Concepts to Understand

These are the things the trainee should be able to explain by the end of the week.

### Chunking
Documents are too long to send to a model in one go. Chunking splits them into smaller pieces. The size of each chunk and how much they overlap with each other affects what the model can see when answering a question.

- **Too small:** chunks lose context (a sentence without the paragraph around it is often meaningless)
- **Too large:** you retrieve less specific content and may exceed the model's context window
- **Overlap:** helps prevent a relevant sentence being split across two chunks where neither chunk alone is useful

### Embeddings and Similarity Search
An embedding is a numerical representation of text that captures its meaning. Two chunks that mean similar things will have embeddings that are close together in vector space. This is what allows retrieval: convert the user's question into an embedding, find the chunks whose embeddings are closest, and those are the most relevant chunks.

### Prompt Construction
The prompt you build for the model matters enormously. A RAG prompt typically looks like:

```
You are an assistant. Answer the user's question using only the context below.
If the answer is not in the context, say you don't know.

Context:
[retrieved chunks go here]

Question:
[user's question]
```

The instruction "only use the context" is what prevents hallucination. Without it, the model will fill gaps with its training knowledge, which may be wrong or outdated.

### Hallucination and Grounding
A model hallucinating means it generates plausible-sounding but incorrect information. In a RAG system, hallucination usually happens when:
- The retrieved chunks don't actually contain the answer
- The prompt doesn't clearly instruct the model to stay within the context
- The model is asked about something not covered by any document

Grounding means anchoring the model's output to real source material. Citations are a grounding technique — if the model must say where it got the answer, it's harder for it to invent one.

---

## Acceptance Criteria

### For the trainee — the system must:
- [ ] Answer questions correctly for at least 70% of the test set
- [ ] Include a source citation (document name and section) with every answer
- [ ] Return a clear "I don't know" when the answer isn't in the documents, rather than guessing
- [ ] Have at least 3 documented chunking/prompt experiments with written observations
- [ ] Include a written evaluation report covering: test set results, failure analysis, and one improvement made

### For the mentor — evaluate on:
| Criterion | What to look for |
|---|---|
| **Understands chunking** | Can explain why they chose their chunk size and what happened when they changed it |
| **Prompt quality** | Prompt clearly grounds the model, handles edge cases (no answer found), and is clean |
| **Honest failure handling** | System says "I don't know" when appropriate — not just for everything or nothing |
| **Evaluation rigor** | Test set covers a range of question types, not just easy ones |
| **Debugging ability** | Can identify *why* a specific question failed, not just that it did |

---

## Common Pitfalls to Watch For

- **Retrieving too few chunks:** top-1 retrieval often misses relevant context. Start with top-3 or top-5.
- **Not cleaning documents:** raw PDFs often have headers, footers, and page numbers mixed into the text. This noise ends up in chunks and confuses retrieval.
- **Testing only easy questions:** a system that only gets tested on questions with obvious answers will look good but fail in production. Require questions where the answer spans multiple sections or where the answer is simply not in the documents.
- **Ignoring latency:** each question triggers at least two API calls (embedding + generation). Trainees should be aware of this and not be surprised when it feels slow.

---

## Stretch Goals (for more experienced trainees)

- Add a **re-ranking step** after retrieval: retrieve top-10 chunks, then use a model to score which are actually relevant before passing to generation
- Implement **hybrid search**: combine semantic (embedding) search with keyword (BM25) search for better coverage
- Add **conversation memory**: allow follow-up questions that refer back to earlier ones ("what about that last policy you mentioned?")
- Expose the system via a simple **REST API** so it could be called by another application

---

## Resources

- watsonx.ai documentation: embedding models and foundation model inference
- LangChain or LlamaIndex docs for RAG pipeline patterns (framework-agnostic concepts apply)
- "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks" — the original RAG paper (Lewis et al., 2020) is worth skimming for context
