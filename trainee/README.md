# Trainee Projects

A structured series of six projects — one engineering-fundamentals check-in plus four AI application projects plus a capstone — for learning AI application development on the IBM watsonx platform. The whole series runs roughly three months. Projects progress from foundational concepts to production-grade systems, culminating in an open-ended capstone built around a real client scenario.

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

### IBM Cloud Account

Create a free IBM Cloud account at [cloud.ibm.com](https://cloud.ibm.com). The sign-up flow will ask for a credit card, but **you will not be charged** — you won't be provisioning any resources directly. The environments you need for the projects will be shared with you.

---

## Structure

Each project lives in its own folder containing the project brief and any mock documents needed to complete it. Projects build on each other — concepts and even code from earlier projects are expected to carry forward.

Each brief lists a set of **milestones** rather than a fixed day-by-day schedule. Work through them in order, at whatever pace gets each one genuinely done — the durations below are targets for the whole project, not a daily itinerary.

---

## The Projects

### Project 0 — Development Environment & Engineering Basics
**Pre-work · 1 day · No AI · Optional**

An optional, ungraded check-in before any AI work begins — skip it if you're already comfortable with the basics. Set up a repo properly, call an external API, handle secrets via environment variables, write a few tests, and use git like it matters. None of this is AI — it exists to confirm the engineering scaffolding is solid before Project 1 introduces AI-specific concepts on top of it.

### Project 1 — Prompting & RAG Foundations
**Tier 1 · 6 days · watsonx.ai**

Build an assistant that answers questions grounded in a set of documents, and can re-express any answer in three different tones — a formal report summary, a casual message, and an executive briefing. Combines the two most fundamental skills in AI application development: retrieval-augmented generation (RAG) for grounding a model in real data, and prompt engineering (system prompts, few-shot examples, structured output, model selection) for controlling how it communicates.

### Project 2 — Agentic Orchestration: Agent + Pipeline
**Tier 2 · 2 weeks · watsonx.ai + watsonx.orchestrate**

Build two orchestrated systems: an HR onboarding **agent** that holds a multi-turn conversation, answers policy questions, submits IT requests, and books orientation sessions — deciding when to act, ask, or escalate — and a customer support triage **pipeline** that classifies, routes, and drafts a response for incoming tickets in a fixed sequence of steps. Building both back to back teaches the most important architectural judgement call in this space: when a problem needs an open-ended reasoning loop versus a fixed sequence of steps. The two weeks cover both getting hands-on with watsonx.orchestrate and building both systems — split however suits you.

### Project 3 — Loan Screening Tool with Governance
**Tier 3 · 2 weeks · watsonx.ai + watsonx.governance**

Build an AI-assisted loan application screener that recommends approve, refer, or decline — then wrap it in a full governance layer. Introduces responsible AI in a regulated domain: explainability, bias detection across protected attributes, decision logging for audit, and producing a model factsheet via watsonx.governance. The first project where accuracy alone is not enough. The two weeks cover both getting hands-on with watsonx.governance and building the screening tool — split between the two however suits you.

### Project 4 — Internal Knowledge Base Agent with Audit Trail
**Tier 3 · 2 weeks · watsonx.ai + watsonx.orchestrate + watsonx.governance**

Build an enterprise-grade internal assistant over a company knowledge base, with role-based document access, PII detection, prompt injection screening, and a tamper-evident audit log of every interaction. Focuses on production readiness: the security and compliance engineering that surrounds the model, not just the model itself. The two weeks cover both platform ramp-up and the build — split between the two however suits you.

### Project 5 — Capstone: Client Brief
**Capstone · ~3.5 weeks · Stack of your choice**

An open-ended project built around a real client scenario chosen from six options (government licensing, Islamic finance, oil & gas field operations, a multi-brand conglomerate's customer care, an electronics retailer's pre-/post-sale support, or municipal complaint handling). No prescribed deliverable structure — the trainee defines scope, designs the architecture, builds a working system, and presents it as they would to a real client. Assessed on problem understanding, design decisions, safety and governance, and the ability to defend choices under questioning.

---

## Progression

```
Pre-work    Tier 1 (Foundation)   Tier 2 (Intermediate)         Tier 3 (Advanced)                Capstone
────────    ───────────────────   ───────────────────────      ─────────────────────────────    ─────────
Project 0   Project 1 · RAG +     Project 2 · Agent + Pipeline  Project 3 · Governance            Project 5
            Prompting                                          Project 4 · Security
```

The tiers reflect increasing complexity in what surrounds the model: from engineering basics, to a single prompt, to an orchestrated agent, to a governed and secured production system.
