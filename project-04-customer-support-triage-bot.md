# Project 4: Customer Support Triage Bot

**Stack:** watsonx.ai + watsonx.orchestrate  
**Duration:** 1 week  
**Difficulty:** Tier 2 — Intermediate

---

## Overview

Build a bot that receives incoming customer support tickets, classifies them by type and urgency, routes them to the correct team, and drafts an initial response to send back to the customer. The bot handles the first 60 seconds of every support interaction — the part that is currently done manually by a triage agent reading each ticket and deciding where it goes.

Where Project 3 focused on a single agent managing a guided conversation, this project introduces a different pattern: a **pipeline**. A ticket comes in, passes through a sequence of model calls (classify → route → draft), and produces a structured output. Each step is a discrete task with its own prompt, its own success criteria, and its own failure mode. The trainee must learn to treat classification and generation as fundamentally different problems — and to make principled decisions about when the pipeline should hand off to a human rather than proceeding automatically.

---

## What to Build

A working triage pipeline with:

1. **Ticket intake** — accept a support ticket as text input (simulated via a file, form, or CLI input)
2. **Classification** — determine the ticket's category (billing, technical, account, general) and urgency (low, medium, high, critical)
3. **Routing** — map the classification to the correct team and flag tickets that require immediate escalation
4. **Response drafting** — generate a personalised first-response email acknowledging the ticket, setting expectations, and providing any immediately useful information
5. **Output** — produce a structured record containing the original ticket, classification, assigned team, and drafted response
6. **A confidence threshold** — tickets where the classifier is uncertain must be flagged for human review rather than routed automatically

The backend (teams, routing rules) should be mocked. A hardcoded routing table is expected and appropriate.

---

## Week Plan

### Day 1 — Understand the problem
- Study the difference between classification tasks and generation tasks — why they need different prompts, different models, and different evaluation methods
- Define the taxonomy: what categories and urgency levels will the system support? Write these down before writing any code
- Collect or write 20–30 sample tickets covering different categories and urgency levels — these will become your test set
- Deliverable: a written taxonomy (categories, urgency levels, routing rules) and a sample ticket dataset

### Day 2 — Build the classifier
- Write a prompt that takes a ticket and returns a category, urgency level, and a confidence score
- Return output as structured JSON: `{ "category": "...", "urgency": "...", "confidence": 0.0–1.0, "reasoning": "..." }`
- Test against your sample tickets — how accurate is it?
- Define a confidence threshold below which the ticket is flagged for human review instead of auto-routed
- Deliverable: a working classifier with structured output and a threshold decision documented

### Day 3 — Build the routing logic and response drafter
- Implement the routing layer: a function that maps category + urgency to an assigned team and SLA (service level agreement)
- Write a prompt that drafts a first-response email: acknowledge the issue, confirm the routing, state when the customer can expect a follow-up, and include any immediately actionable advice for common issues
- Ensure the draft is personalised to the ticket — it must not be a generic template that ignores the customer's specific problem
- Deliverable: routing logic and a response drafter that produces distinct, relevant drafts for different ticket types

### Day 4 — Wire the pipeline together and handle edge cases
- Connect all three steps: intake → classify → route → draft → output
- Handle the low-confidence path: tickets below the threshold produce a different output (flagged for human review, no auto-routing, no draft sent)
- Test with edge cases: ambiguous tickets, tickets in a language other than English, very short tickets ("it's broken"), tickets that span multiple categories
- Deliverable: an end-to-end pipeline with structured output for both the auto-routed and human-review paths

### Day 5 — Evaluate, measure latency and cost, and reflect
- Run your full test set of 20–30 tickets through the pipeline and score classification accuracy
- Measure the latency and estimated token cost per ticket — calculate what this would cost at 1,000 tickets per day
- Identify at least 3 failure cases and document what caused each one
- Write a short reflection: where did you set your confidence threshold and why? What would you change?
- Deliverable: evaluation report with accuracy score, cost estimate, failure analysis, and threshold justification

---

## Key Concepts to Understand

These are the things the trainee should be able to explain by the end of the week.

### Classification vs. Generation

These are not just different tasks — they require a different mindset:

| | Classification | Generation |
|---|---|---|
| **Output** | One of a fixed set of labels | Free-form text |
| **Evaluation** | Accuracy, precision, recall — objective | Quality, relevance, tone — subjective |
| **Failure mode** | Wrong label (silent, easy to miss) | Bad text (visible, easy to notice) |
| **Prompt goal** | Force the model to choose | Guide the model to create |
| **Model size** | Often works well with smaller models | Usually benefits from larger models |

The classification step should be evaluated quantitatively against known-correct labels. The generation step requires human judgement and qualitative review.

### Structured Output from a Classifier

A classifier that returns plain text ("this is a billing issue") is hard to use programmatically. The pipeline needs structured output — JSON with defined fields — so the routing logic can parse it reliably. The prompt must be explicit about the schema, and the pipeline must validate the output before passing it downstream.

A classifier that also returns a `confidence` field and a `reasoning` field is significantly more useful:
- Confidence enables the threshold logic (route automatically vs. flag for human)
- Reasoning makes failures debuggable — you can see *why* the model made the wrong call

### Confidence Thresholds

Not every ticket should be handled automatically. A confidence threshold is the mechanism for deciding when the model is uncertain enough that a human should take over. Setting the threshold requires a deliberate tradeoff:

- **Too high:** most tickets are flagged for human review, defeating the purpose of automation
- **Too low:** uncertain classifications are routed incorrectly, sending customers to the wrong team

The right threshold depends on the cost of a wrong routing vs. the cost of manual review. In a real system, this would be tuned based on historical data. In this project, the trainee should define the threshold explicitly and justify it.

### Multi-Step Pipeline Design

When multiple model calls are chained together, failures compound. If the classifier returns a malformed response, the router breaks. If the router produces an unexpected team name, the drafter may not have the right context. Each step must:

1. Validate its input before processing
2. Produce output in a defined, predictable format
3. Handle failures explicitly — don't let an error in step 2 silently corrupt step 3

Think of each step as a function with a contract: defined inputs, defined outputs, defined error behaviour.

### Latency and Cost Budgeting

A pipeline with three model calls has three times the latency and three times the cost of a single call (approximately). At scale, this matters. The trainee should understand:

- Which step uses the most tokens (likely the response drafter, which generates the longest output)
- Whether any step could use a smaller, cheaper model without sacrificing quality
- What the per-ticket cost implies at realistic support volumes (100/day, 1,000/day, 10,000/day)

This is not about optimising prematurely — it is about building cost awareness as a habit before it becomes a production surprise.

### Human-in-the-Loop as a Design Feature

A system that routes everything automatically is not more capable than one with a human fallback — it is more brittle. The human-in-the-loop path is not a failure mode; it is a deliberate design decision that makes the system safer and more trustworthy. The trainee should be able to articulate what goes into the human-review queue and why, not treat it as a fallback for when things go wrong.

---

## Acceptance Criteria

### For the trainee — the system must:
- [ ] Correctly classify at least 80% of tickets in the test set by category
- [ ] Correctly classify at least 75% of tickets by urgency level
- [ ] Flag tickets below the confidence threshold for human review rather than auto-routing them
- [ ] Produce a draft response that is visibly personalised to the ticket — not a generic template
- [ ] Include a structured output record for every ticket (auto-routed and flagged paths)
- [ ] Include an evaluation report with: accuracy scores, cost estimate per ticket, at least 3 failure cases, and a written threshold justification

### For the mentor — evaluate on:
| Criterion | What to look for |
|---|---|
| **Classification quality** | Prompt returns valid JSON consistently; category and urgency labels match the defined taxonomy |
| **Threshold reasoning** | Trainee can explain where they set the threshold and the tradeoff they made |
| **Pipeline resilience** | Each step validates its input; a failure in one step doesn't silently corrupt downstream steps |
| **Response personalisation** | Draft responses address the customer's specific issue, not a generic acknowledgement |
| **Cost awareness** | Trainee has calculated per-ticket cost and can identify which step is most expensive |

---

## Sample Ticket Dataset

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

## Routing Table

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

## Common Pitfalls to Watch For

- **Taxonomy drift:** if the classifier prompt doesn't exactly match the defined categories and urgency levels, the model will invent its own labels. The prompt must enumerate the exact allowed values.
- **Confidence scores are not probabilities:** a model that returns `"confidence": 0.9` is not necessarily right 90% of the time — it is expressing a relative degree of certainty. Trainees should calibrate their threshold empirically against the test set, not assume a number means what it sounds like.
- **Generic draft responses:** the most common failure in the generation step is a draft that could apply to any ticket. The prompt must explicitly instruct the model to reference the customer's specific problem.
- **Silent routing errors:** if the classifier returns a category not in the routing table, the routing step will fail. This must be handled explicitly — unknown categories should fall through to the human-review path.
- **Testing only clean tickets:** real support tickets are messy. Ticket 10 in the sample set ("it doesnt work fix it") is representative. The pipeline must handle ambiguous, short, and poorly written inputs without breaking.

---

## Stretch Goals (for more experienced trainees)

- Add a **duplicate detection step**: before routing, check whether an incoming ticket is substantially similar to a recently submitted one from the same customer, and flag it as a potential duplicate
- Implement **sentiment analysis** as a secondary signal: a customer who is clearly angry should have their urgency bumped by one level regardless of the technical content of the ticket
- Add **batch processing**: accept a CSV of tickets and process them all, outputting a structured results file — then calculate aggregate statistics (category distribution, average confidence, flagging rate)
- Explore **prompt chaining vs. single prompt**: try collapsing classification and response drafting into a single prompt and compare quality and cost against the two-step pipeline

---

## Resources

- watsonx.ai documentation: structured output, JSON mode, and model parameters
- watsonx.orchestrate documentation: pipeline design and multi-step skill orchestration
- "Evaluating Large Language Models: A Survey" — useful background on classification evaluation metrics (precision, recall, F1)
