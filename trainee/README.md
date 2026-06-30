# Trainee Projects

A structured series of seven projects for learning AI application development on the IBM watsonx platform. Projects progress from foundational concepts to production-grade systems, culminating in an open-ended capstone built around a real client scenario.

---

## Before You Start

Complete the following **before starting any of the projects**.

### IBM SkillsBuild Courses

> **You will need an IBM SkillsBuild account to access these courses.** Create one for free at [skills.yourlearning.ibm.com](https://skills.yourlearning.ibm.com) before opening the links below.

| Course | Link |
|---|---|
| Getting Started with Generative AI | [Open course](https://skills.yourlearning.ibm.com/activity/PLAN-BAEFCCAAD520?ngo-id=0302) |
| Mastering the Art of Prompting | [Open course](https://skills.yourlearning.ibm.com/activity/ALM-COURSE_4058858?ngo-id=0302) |
| Make Agentic AI Work for You | [Open course](https://skills.yourlearning.ibm.com/activity/PLAN-37BFD561DC25?ngo-id=0302) |

### Reference Book

**AI Engineering: Building Applications with Foundation Models** — Chip Huyen (O'Reilly)

A comprehensive reference covering foundation models, prompt engineering, RAG, agents, evaluation, and production deployment. Use it to go deeper on any topic you encounter across the projects. The full book is available in this folder as `AI Engineering.pdf`.

---

## Structure

Each project lives in its own folder containing the project brief and any mock documents needed to complete it. Projects build on each other — concepts and even code from earlier projects are expected to carry forward.

---

## The Projects

### Project 1 — Document Q&A with RAG
**Tier 1 · 1 week · watsonx.ai**

Build an assistant that answers questions grounded in a set of documents. Introduces the two most fundamental concepts in AI application development: prompt engineering and retrieval-augmented generation (RAG). The trainee learns how to chunk documents, generate embeddings, retrieve relevant context, and construct prompts that prevent hallucination.

### Project 2 — Multi-Tone Content Generator
**Tier 1 · 1 week · watsonx.ai**

Build a tool that takes a single input and produces three versions of it in different tones — a formal report summary, a casual social post, and an executive briefing. A focused deep-dive into prompt engineering: system prompts, few-shot examples, structured output, and model selection tradeoffs.

### Project 3 — HR Onboarding Agent
**Tier 2 · 1 week · watsonx.ai + watsonx.orchestrate**

Build a conversational agent that guides new hires through onboarding. The agent answers policy questions, submits IT access requests, and books orientation sessions — deciding which tool to call and when to ask the user for confirmation. Introduces agentic systems: the reasoning loop, tool definitions, stateful conversation, and the boundary between acting autonomously and escalating to a human.

### Project 4 — Customer Support Triage Bot
**Tier 2 · 1 week · watsonx.ai + watsonx.orchestrate**

Build a pipeline that receives a support ticket and classifies it, routes it to the correct team, and drafts a personalised first response. Introduces multi-step pipeline design, the difference between classification and generation tasks, confidence thresholds, and human-in-the-loop as a deliberate design decision rather than a fallback.

### Project 5 — Loan Screening Tool with Governance
**Tier 3 · 1 week · watsonx.ai + watsonx.governance**

Build an AI-assisted loan application screener that recommends approve, refer, or decline — then wrap it in a full governance layer. Introduces responsible AI in a regulated domain: explainability, bias detection across protected attributes, decision logging for audit, and producing a model factsheet via watsonx.governance. The first project where accuracy alone is not enough.

### Project 6 — Internal Knowledge Base Agent with Audit Trail
**Tier 3 · 1 week · watsonx.ai + watsonx.orchestrate + watsonx.governance**

Build an enterprise-grade internal assistant over a company knowledge base, with role-based document access, PII detection, prompt injection screening, and a tamper-evident audit log of every interaction. Focuses on production readiness: the security and compliance engineering that surrounds the model, not just the model itself.

### Project 7 — Capstone: Client Brief
**Capstone · 2 weeks · Stack of your choice**

An open-ended project built around a real client scenario chosen from six options (government licensing, Islamic finance, oil & gas field operations, hospital triage, legal contract review, or municipal complaint handling). No prescribed deliverable structure — the trainee defines scope, designs the architecture, builds a working system, and presents it as they would to a real client. Assessed on problem understanding, design decisions, safety and governance, and the ability to defend choices under questioning.

---

## Progression

```
Tier 1 (Foundation)       Tier 2 (Intermediate)      Tier 3 (Advanced)         Capstone
─────────────────────     ──────────────────────     ─────────────────────     ─────────
Project 1 · RAG           Project 3 · Agent          Project 5 · Governance    Project 7
Project 2 · Prompting     Project 4 · Pipeline       Project 6 · Security
```

The tiers reflect increasing complexity in what surrounds the model: from a single prompt, to an orchestrated agent, to a governed and secured production system.
