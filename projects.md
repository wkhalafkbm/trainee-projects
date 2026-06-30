# Trainee Project Ideas — IBM watsonx Stack

Projects for interns and trainees learning to build AI applications using watsonx.ai, watsonx.orchestrate, and watsonx.governance.

---

## Tier 1 — Foundation (watsonx.ai)

### 1. Document Q&A with RAG — [full brief](project-01-rag-document-qa.md)
**What they build:** An assistant that answers questions over a set of company documents (PDFs, internal wikis).

**What they learn:**
- Prompt engineering — how prompt structure affects output quality
- Chunking strategy and embedding tradeoffs in RAG pipelines
- Grounding LLM responses in facts vs. hallucination risk
- When to use semantic search vs. keyword search

**Proof of learning:** Ask them to break their own RAG system — find a question it answers incorrectly and explain why, then fix it.

---

### 2. Multi-Tone Content Generator — [full brief](project-02-multi-tone-content-generator.md)
**What they build:** A tool that takes a topic and generates content in different tones (formal report, casual social post, executive summary).

**What they learn:**
- System prompts vs. user prompts and their scope
- Few-shot prompting techniques
- Output formatting and structured generation (JSON, markdown)
- Model selection tradeoffs (cost vs. capability)

---

## Tier 2 — Intermediate (watsonx.ai + orchestrate)

### 3. HR Onboarding Agent — [full brief](project-03-hr-onboarding-agent.md)
**What they build:** An agent that guides new hires through onboarding — answers policy questions, submits IT requests, books orientation sessions.

**What they learn:**
- Tool/skill definition in watsonx.orchestrate
- Agentic loop design — when the model should act vs. ask vs. escalate
- Stateful conversation management
- Failure modes: tool call errors, ambiguous user intent, infinite loops

**Key lesson:** agents need guardrails on what they can do autonomously vs. what requires human approval.

---

### 4. Customer Support Triage Bot — [full brief](project-04-customer-support-triage-bot.md)
**What they build:** A bot that classifies incoming support tickets, routes them to the right team, and drafts an initial response.

**What they learn:**
- Classification vs. generation as separate tasks
- Orchestrating multiple model calls in a pipeline
- Confidence thresholds — when to fall back to a human
- Latency and cost budgeting across a multi-step flow

---

## Tier 3 — Advanced (Full Stack + watsonx.governance)

### 5. Loan/Credit Application Screening Tool (with Governance) — [full brief](project-05-loan-screening-governance.md)
**What they build:** A system that uses an AI model to assist in evaluating loan applications, with full governance tracking.

**What they learn:**
- Bias detection and fairness metrics (critical for financial AI)
- Explainability — the model must justify every decision
- watsonx.governance model cards, factsheets, and monitoring dashboards
- Regulatory thinking: what decisions can't be fully delegated to AI

**Proof of learning:** They must produce a governance report showing the model's risk profile and at least one bias finding they mitigated.

---

### 6. Internal Knowledge Base Agent with Audit Trail — [full brief](project-06-knowledge-base-agent-audit.md)
**What they build:** An enterprise-grade internal assistant (like a smarter intranet search) that logs every interaction for audit purposes.

**What they learn:**
- PII detection and data handling before sending content to a model
- Logging, tracing, and monitoring in production AI systems
- Prompt injection awareness and input sanitization
- watsonx.governance for tracking model usage and drift over time

---

## Capstone

### 7. Capstone — Client Brief — [full brief](project-07-capstone.md)
**What they build:** Trainees choose from six realistic business scenarios and design, build, and present a solution end to end — no prescribed architecture, no week plan, no sample data provided.

**What it tests:** Problem interpretation, architecture decision-making, scope management, safety and governance design, and the ability to present and defend decisions under questioning.

**Duration:** 2 weeks

**Mentor resources:** [Evaluator guide](project-07-evaluator-guide.md) (do not share with trainees) | Mock documents: [`project-07-mock-docs/`](project-07-mock-docs/)

---

## Cross-Cutting Requirements

Regardless of which project a trainee picks, require them to demonstrate:

| Concern | What to demonstrate |
|---|---|
| **Evaluation** | A test set with at least 20 cases and a scoring methodology |
| **Failure analysis** | Document 3 ways the system can fail and how they handled it |
| **Governance** | A factsheet or model card for their deployed model |
| **Cost awareness** | Token usage estimate and how they optimized it |
| **Human-in-the-loop** | At least one point where the system defers to a human |
