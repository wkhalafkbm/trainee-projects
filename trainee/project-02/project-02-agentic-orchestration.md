# Project 2: Agentic Orchestration — Agent + Pipeline

**Stack:** watsonx.ai + watsonx.orchestrate
**Duration:** 2 weeks (platform/lab ramp-up and build, split as needed)
**Difficulty:** Tier 2 — Intermediate
**Mock documents:** [`mock-docs/`](mock-docs/)

---

## Overview

Build two orchestrated systems on watsonx.orchestrate that represent the two fundamental patterns for putting a model in charge of more than a single reply: an **agent** that holds a multi-turn conversation and decides what to do next, and a **pipeline** that runs a fixed sequence of steps over a single input.

**Part A** is an HR onboarding agent: it guides new hires through onboarding, answering policy questions, submitting IT access requests, and booking orientation sessions — deciding which tool to call and when to ask the user for confirmation.

**Part B** is a customer support triage bot: it receives a support ticket, classifies it, routes it to the correct team, and drafts an initial response — a sequence of discrete steps, each with its own prompt and its own failure mode.

Building both back to back, under the same platform, is the point. The most important architectural judgement call in AI application development is knowing *when a problem needs an open-ended reasoning loop and when it needs a fixed sequence of steps* — and that judgement is much easier to develop once you've built one of each and can compare them directly.

---

## What to Build

### Part A — HR Onboarding Agent
1. **A conversational interface** — the new hire interacts with the agent via chat (CLI or simple UI)
2. **A policy Q&A skill** — the agent answers questions about HR policies using the mock document set (can reuse RAG concepts from Project 1)
3. **An IT request skill** — the agent collects required information and submits a mock IT access request (writing to a file or a simple data store is sufficient)
4. **A session booking skill** — the agent checks available orientation slots and books one on behalf of the user (a hardcoded schedule is fine)
5. **A guardrail layer** — certain actions require the agent to confirm with the user before proceeding

### Part B — Support Triage Pipeline
1. **Ticket intake** — accept a support ticket as text input (simulated via a file, form, or CLI input)
2. **Classification** — determine the ticket's category (billing, technical, account, general) and urgency (low, medium, high, critical), with a confidence score
3. **Routing** — map the classification to the correct team and flag tickets that require immediate escalation
4. **Response drafting** — generate a personalised first-response email
5. **A confidence threshold** — tickets where the classifier is uncertain must be flagged for human review rather than routed automatically

### Closing deliverable — Agent vs. Pipeline
A short written comparison: for each system, why did it need the architecture it got? What would break if you swapped them — ran onboarding as a fixed pipeline, or triage as an open-ended agent?

Mock backends are expected and appropriate throughout. The focus is the orchestration logic, not production-grade integrations.

---

## Milestones

Work through these in order. There is no fixed day-by-day schedule — move at the pace that gets each milestone genuinely done, not just checked off.

### Milestone 1 — Understand agentic and pipeline systems
- Read about the ReAct pattern (Reasoning + Acting): how an agent decides which tool to call, calls it, observes the result, and decides what to do next
- Read about the difference between classification tasks and generation tasks — why they need different prompts, different models, and different evaluation methods
- Study how watsonx.orchestrate defines skills and routes between them
- Map out both systems on paper before building either: what can the agent do and what could go wrong; what taxonomy (categories, urgency levels, routing rules) will the pipeline use
- Collect or write 20–30 sample support tickets covering different categories and urgency levels — these become your Part B test set
- Deliverable: a decision-flow diagram for the agent, a written taxonomy for the pipeline, and a sample ticket dataset

### Milestone 2 — Build the policy Q&A skill (Part A)
- Use the mock HR documents in `mock-docs/` (leave policy, IT access policy, code of conduct, benefits guide, orientation guide)
- Build a retrieval-backed skill that answers policy questions (a lightweight version of Project 1)
- Wire it into the orchestrate environment as a callable skill
- Deliverable: a skill the agent can invoke to answer "what is the leave policy?" style questions

### Milestone 3 — Build the IT request and session booking skills (Part A)
- IT request skill: the agent must collect the new hire's name, role, and required systems before submitting — asking follow-up questions if any are missing
- Session booking skill: present available slots, confirm the user's choice, and write the booking to a simple store
- Deliverable: two working skills, each testable in isolation before being wired to the agent

### Milestone 4 — Wire the agent together and add guardrails (Part A)
- Connect all three skills to the orchestration layer
- Define which actions require explicit user confirmation before the agent proceeds (booking a session and submitting an IT request should both require confirmation)
- Test multi-turn conversations end to end: a new hire who asks a policy question, then requests IT access, then books a session in a single conversation
- Deliverable: a working end-to-end agent that handles a full onboarding conversation

### Milestone 5 — Build the classifier (Part B)
- Write a prompt that takes a ticket and returns a category, urgency level, and a confidence score as structured JSON: `{ "category": "...", "urgency": "...", "confidence": 0.0–1.0, "reasoning": "..." }`
- Test against your sample tickets — how accurate is it?
- Define a confidence threshold below which the ticket is flagged for human review instead of auto-routed
- Deliverable: a working classifier with structured output and a documented threshold decision

### Milestone 6 — Build routing and response drafting, wire the pipeline (Part B)
- Implement the routing layer: a function that maps category + urgency to an assigned team and SLA
- Write a prompt that drafts a first-response email — it must reference the customer's specific problem, not a generic acknowledgement
- Connect intake → classify → route → draft → output; handle the low-confidence path (flagged for human review, no auto-routing, no draft sent)
- Test with edge cases: ambiguous tickets, very short tickets ("it's broken"), tickets spanning multiple categories
- Deliverable: an end-to-end pipeline with structured output for both the auto-routed and human-review paths

### Milestone 7 — Test failure modes across both systems
- Agent: deliberately trigger infinite loops, ambiguous tool selection, missing required inputs, and out-of-scope requests — document how the agent behaves and fix at least two failure modes
- Pipeline: deliberately trigger taxonomy drift, silent routing errors, and generic draft responses — document how the pipeline behaves and fix at least two failure modes
- Deliverable: a failure-mode report covering both systems

### Milestone 8 — Evaluate, compare architectures, and reflect
- Run the pipeline's full ticket test set and score classification accuracy by category and urgency; measure latency and estimated token cost per ticket, and what that implies at 1,000 tickets/day
- Write a short reflection on the agent: what decisions did you make about what it can do autonomously vs. what requires human approval, and why?
- Write the closing comparison: why does onboarding need an agent and triage need a pipeline? What would happen if you swapped the two patterns?
- Deliverable: evaluation report (pipeline accuracy, cost, failure analysis, threshold justification) and the agent-vs-pipeline reflection

---

## Key Concepts to Understand

These are the things you should be able to explain by the end.

### The Agentic Loop
A traditional model call is a single exchange: input in, output out. An agent runs a loop — **think** (what should I do next?), **act** (call a tool or ask the user), **observe** (receive the result), **repeat** — until it decides the task is complete. Most agent bugs happen at the boundaries: the agent acts when it should ask, or gets stuck because it can't interpret a tool result.

### Tool/Skill Definition
Each skill needs a name and description (the model uses this to decide when to call it), an input schema, and an output schema. A vague or overlapping description is the most common source of an agent calling the wrong skill.

### Act vs. Ask vs. Escalate
- **Act autonomously:** low-stakes, reversible, or clearly within the user's stated intent
- **Ask for confirmation:** actions with side effects that are hard to reverse
- **Escalate to a human:** anything outside the agent's defined scope, or where it's uncertain and the stakes are high

It's tempting to make agents more autonomous because it feels more impressive. A good agent knows its limits instead.

### Stateful Conversation Management
An agent needs to remember earlier turns. Critical state (name, role, selections made) should be tracked explicitly in the application layer rather than relying on the model to extract it from a long history — the longer the history, the more tokens each turn costs, and the less reliable extraction becomes.

### Classification vs. Generation
These require a different mindset. Classification output is one of a fixed set of labels, evaluated with accuracy/precision/recall, and its failure mode (a wrong label) is silent and easy to miss. Generation output is free-form text, evaluated with human judgement, and its failure mode (bad text) is visible. The classification step should be evaluated quantitatively; the generation step needs qualitative review.

### Confidence Thresholds
A threshold is the mechanism for deciding when a classifier is uncertain enough that a human should take over. Too high, and most tickets get flagged, defeating the purpose of automation. Too low, and uncertain classifications get routed incorrectly. A confidence score is not a probability — calibrate the threshold empirically against your test set, not by assuming what the number sounds like it means.

### Multi-Step Pipeline Design
When model calls are chained, failures compound. Each step must validate its input, produce output in a defined format, and handle failures explicitly — an error in one step should never silently corrupt the next. Think of each step as a function with a contract.

### Latency and Cost Budgeting
A pipeline with three model calls costs roughly three times a single call, in both time and money. Know which step uses the most tokens, whether any step could use a cheaper model without sacrificing quality, and what the per-ticket cost implies at realistic volumes.

### Human-in-the-Loop as a Design Feature
A system that routes or acts on everything automatically is more brittle, not more capable, than one with a human fallback. The human-review path is a deliberate design decision, not a failure mode — you should be able to articulate what goes into it and why, for both the agent and the pipeline.

### Failure Modes in Agentic and Pipeline Systems
Agents fail through infinite loops, ambiguous tool selection, missing required inputs, and hallucinated tool parameters. Pipelines fail through taxonomy drift (the model inventing labels outside the defined set), silent routing errors on unknown categories, and generic outputs that ignore the specific input. Both classes of failure share a root cause worth noticing: the system trusted the model's output without validating it against a defined contract.

### Choosing Agent vs. Pipeline
An agent is the right shape when the sequence of steps depends on what the user says and can't be fully predicted in advance — the model has to *decide* what happens next. A pipeline is the right shape when the sequence of steps is always the same regardless of input — the model just has to *execute* well at each fixed step. Reaching for an agent when a pipeline would do adds unpredictability and cost for no benefit; reaching for a pipeline when the task genuinely needs multi-turn, user-driven decisions produces a rigid system that can't handle real conversations.

---

## Acceptance Criteria

### The system must:

**Part A — Agent:**
- [ ] Handle a full onboarding conversation covering all three capabilities (policy Q&A, IT request, session booking) without breaking
- [ ] Ask for user confirmation before submitting the IT request or booking a session
- [ ] Ask follow-up questions when required information is missing rather than proceeding with incomplete data or making something up
- [ ] Respond gracefully to out-of-scope questions — acknowledge it can't help rather than attempting an answer

**Part B — Pipeline:**
- [ ] Correctly classify at least 80% of tickets in the test set by category, and 75% by urgency level
- [ ] Flag tickets below the confidence threshold for human review rather than auto-routing them
- [ ] Produce a draft response that is visibly personalised to the ticket — not a generic template
- [ ] Include a structured output record for every ticket (auto-routed and flagged paths)

**Both:**
- [ ] Include a written failure-mode report covering at least 3 scenarios per system and how they were addressed
- [ ] Include the closing written comparison of why each system uses its architecture and what would break if swapped

---

## Common Pitfalls to Watch For

- **Overlapping skill descriptions:** if the IT request skill and the policy Q&A skill both mention "employee information," the agent may confuse them.
- **No confirmation before side effects:** an agent that submits requests or books sessions without asking is a design flaw, not a missing feature.
- **Relying on the model to remember everything:** track critical conversation state explicitly in the application layer.
- **Only testing the happy path:** test messy inputs — vague requests, missing information, topic changes mid-conversation, ambiguous or very short tickets.
- **Taxonomy drift:** if the classifier prompt doesn't exactly match the defined categories and urgency levels, the model will invent its own. Enumerate the exact allowed values in the prompt.
- **Generic draft responses:** the most common pipeline failure — the prompt must explicitly instruct the model to reference the customer's specific problem.
- **Silent routing errors:** if the classifier returns a category not in the routing table, this must be handled explicitly, falling through to human review.
- **Not defining an exit condition for the agent:** without a clear "done" state, the agent may keep asking questions after the task is finished.

---

## Stretch Goals (for more experienced trainees)

- Agent: add an **escalation path** to a human HR representative for out-of-scope requests, and a **confidence threshold** on the policy Q&A skill's retrieval scores
- Pipeline: add **duplicate detection** for tickets and **sentiment analysis** as a secondary urgency signal
- Explore **parallel tool calls** in the agent, and **prompt chaining vs. single-prompt** collapsing in the pipeline — compare quality and cost against the multi-step version
- Add **batch processing** to the pipeline: accept a CSV of tickets, process them all, and calculate aggregate statistics

---

## Sample Ticket Dataset (Part B)

Use these tickets to build and test the pipeline. They span all categories and urgency levels and include several edge cases.

---

**Ticket 1**
> "I was charged twice for my subscription this month. I need this fixed immediately — I can't afford to have money taken from my account like this."

Expected: Category: Billing | Urgency: High

---

**Ticket 2**
> "Hi, just wondering if you offer student discounts? No rush."

Expected: Category: Billing | Urgency: Low

---

**Ticket 3**
> "The application crashes every time I try to export a report. I've tried reinstalling but the problem persists. This is blocking my entire team from closing month-end."

Expected: Category: Technical | Urgency: Critical

---

**Ticket 4**
> "I forgot my password and the reset email isn't arriving. I've checked spam."

Expected: Category: Account | Urgency: Medium

---

**Ticket 5**
> "Everything is down. None of our staff can log in. We have a client presentation in 2 hours."

Expected: Category: Technical | Urgency: Critical

---

**Ticket 6**
> "How do I change the email address on my account?"

Expected: Category: Account | Urgency: Low

---

**Ticket 7**
> "I cancelled my subscription 3 weeks ago but I was still charged this month. I want a refund and I want to know why this happened."

Expected: Category: Billing | Urgency: High

---

**Ticket 8**
> "The export feature is a bit slow sometimes. Not urgent, just flagging it."

Expected: Category: Technical | Urgency: Low

---

**Ticket 9**
> "I need to transfer my account to a different email address because I'm changing companies. I also need an invoice for the last 12 months for my accountant."

Expected: Category: Account + Billing (multi-category — should trigger human review or pick primary) | Urgency: Medium

---

**Ticket 10**
> "it doesnt work fix it"

Expected: Category: Technical (low confidence — should flag for human review) | Urgency: Unknown

---

Add at least 10 more tickets of your own covering remaining category and urgency combinations before running your final evaluation.

---

## Routing Table (Part B)

Use this routing table as the mock backend for the routing step.

| Category | Urgency | Assigned Team | SLA |
|---|---|---|---|
| Billing | Critical | Billing — Senior | 1 hour |
| Billing | High | Billing — Standard | 4 hours |
| Billing | Medium | Billing — Standard | 1 business day |
| Billing | Low | Billing — Standard | 3 business days |
| Technical | Critical | Engineering — On-call | 30 minutes |
| Technical | High | Engineering — Support | 2 hours |
| Technical | Medium | Engineering — Support | 1 business day |
| Technical | Low | Engineering — Backlog | 5 business days |
| Account | High | Customer Success | 4 hours |
| Account | Medium | Customer Success | 1 business day |
| Account | Low | Customer Success | 3 business days |
| General | Any | Customer Success | 2 business days |
| Flagged for review | Any | Triage — Human | Immediate |

---

## Resources

- watsonx.orchestrate documentation: skill definition, agent configuration, pipeline design, and conversation management
- "ReAct: Synergizing Reasoning and Acting in Language Models" (Yao et al., 2022) — the foundational paper behind most agentic frameworks
- watsonx.ai documentation: tool use, function calling, structured output, and JSON mode
- "Evaluating Large Language Models: A Survey" — useful background on classification evaluation metrics (precision, recall, F1)
