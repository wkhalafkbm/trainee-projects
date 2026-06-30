# Project 7: Capstone — Client Brief

**Stack:** Your choice  
**Duration:** 2 weeks  
**Difficulty:** Capstone  
**Mock documents:** [`project-07-mock-docs/`](project-07-mock-docs/) — one subfolder per scenario

---

## What This Project Is

The previous six projects gave you a problem, a plan, and told you what to build. This one does not.

A client has come to you with a business problem. Your job is to understand it, decide what to build, design the system, build it, and present it — the same way you would in a real engagement. The client brief is intentionally vague in places. That is not an oversight. Part of what you are being assessed on is how you handle ambiguity: the questions you ask, the assumptions you make explicit, and the decisions you justify.

You will choose one scenario from the list below. No two trainees in the same cohort may choose the same one.

---

## What You Must Produce

Unlike earlier projects, there is no prescribed deliverable structure. You decide what to build and how to present it. At minimum, your submission must include:

### 1. Discovery Document

Before writing any code, produce a one-to-two page document covering:

- Your interpretation of the client's problem — what are they actually trying to solve?
- The questions you would ask the client before starting (and your assumed answers)
- What is in scope for your solution and what is explicitly out of scope
- The risks and constraints you identified

This is the most important document in your submission. A solution built on a wrong reading of the problem is worthless no matter how well it is built.

### 2. Architecture Diagram

A diagram showing the components of your system, how data flows between them, and where each watsonx product fits. Hand-drawn is acceptable. The diagram must be accompanied by a written explanation of why you made the architectural choices you did — not just what you built, but why you built it that way.

### 3. Working System

A functional implementation of your solution. It does not need to be complete — scoping is part of the exercise. What it does need is to demonstrate the core AI capability, at least one governance or safety mechanism, and enough end-to-end flow that a reviewer can see it working.

### 4. Test Evidence

Show that your system works and that you tried to break it. At minimum: a set of test cases covering the happy path, at least two edge cases, and at least one failure case with an explanation of why it fails and what you would do about it given more time.

### 5. Presentation (15 minutes)

Present your solution to your mentor as if you are presenting to the client. Cover: what you built, why you built it this way, what works, what doesn't, and what you would do next. You will be asked questions. The ability to defend your decisions under questioning is part of the assessment.

---

## The Client Scenarios

---

### Scenario A — Ministry of Commerce: Business Licensing Assistant

**The brief:**

> "We handle hundreds of enquiries every day from business owners asking about licensing requirements, required documents, fees, and renewal procedures. Our staff spend most of their time answering the same questions repeatedly instead of handling complex cases. We want an AI assistant that can handle routine enquiries so our staff can focus on the work that actually needs a human. We have a large internal manual that covers most of what people ask about, but it hasn't been updated consistently and some sections are outdated. We also want to make sure we know what the AI is telling people — if it gives wrong advice about a legal requirement, that is a serious problem for us."

**What to think about:** What happens when the AI's source documents are outdated? Who is liable when AI gives incorrect regulatory guidance? What queries absolutely must not be handled without a human? How do you build trust with a government client who has never deployed AI before?

---

### Scenario B — Burgan-style Retail Bank: Islamic Finance Product Advisor

**The brief:**

> "Our customers often don't understand the difference between our Murabaha, Ijara, and Tawarruq products. They call our contact centre, wait on hold, and still leave confused. We want a digital assistant that can explain our products in plain language, help customers understand which product might suit their situation, and guide them to apply. We are a regulated entity — we cannot give financial advice, and we cannot make promises about approval. The assistant must stay within those boundaries. We also have customers who speak Arabic and customers who speak English, sometimes in the same message."

**What to think about:** Where is the line between product information and financial advice? How do you handle code-switching (Arabic/English in the same query)? What does "cannot make promises about approval" mean for the system's outputs? What governance is required for a financial services AI in Kuwait?

---

### Scenario C — Kuwait Oil Company Field Operations

**The brief:**

> "Our field engineers carry hundreds of technical manuals, maintenance procedures, and safety protocols. When something goes wrong at 2am, they need answers fast and they cannot search through PDFs on a tablet in the dark. We want a mobile-friendly assistant that can answer questions from our technical documentation. The safety-critical part is important: some of our procedures have very specific steps that must be followed in order, and an AI that paraphrases or skips a step could cause an accident. We also have documentation at different sensitivity levels — general maintenance procedures are fine to share widely, but some operational data is restricted to senior engineers."

**What to think about:** How do you handle procedural content where order and completeness matter? What does "paraphrasing" a safety procedure mean for the system design? How do you implement document-level access control? What does a failure in this system look like, and what is the cost?

---

### Scenario D — Private Hospital: Patient Intake and Triage

**The brief:**

> "Patients arrive at our reception or call our helpline describing symptoms, and our front-desk staff have to decide which department to route them to. We want an AI assistant to handle this triage step — take a description of symptoms from the patient, ask follow-up questions if needed, and route them to the right department with a summary for the receiving nurse. We are very aware that this is a medical context and that a wrong routing could delay critical care. We are not asking the AI to diagnose anyone. We want it to route, not diagnose. We need to be able to show our medical director exactly what the AI asked, what the patient said, and what routing decision was made for every single interaction."

**What to think about:** What is the difference between routing and diagnosing, and where is the line technically? What happens when a patient describes a potentially life-threatening symptom? How do you design an AI system where the cost of a false negative (routing a critical patient to the wrong department) is extremely high? What does the audit trail need to contain to satisfy a medical director?

---

### Scenario E — Law Firm: Contract Review and Compliance Flagging

**The brief:**

> "We review a large number of commercial contracts and our junior associates spend significant time on first-pass review — identifying non-standard clauses, missing provisions, and potential compliance issues under Kuwait Commercial Law. We want a tool that can do this first pass and flag items for a senior associate to review. It should not give legal opinions — it should flag and summarise, not conclude. Confidentiality is critical: our clients' contracts must never be processed in a way that could expose them to a competitor or to any third party. We also need to know which version of a clause the AI was trained to recognise — the law changes and we need to be able to update it."

**What to think about:** How do you build a document review tool that flags without concluding? What does "confidentiality" mean technically for data sent to a model API? How do you version the knowledge the AI uses so it can be updated when the law changes? How do you handle a contract written partly in Arabic and partly in English?

---

### Scenario F — Kuwait Municipality: Public Services Complaint Handler

**The brief:**

> "We receive thousands of complaints and service requests from the public every week — potholes, broken streetlights, waste collection issues, noise complaints. Right now everything comes in through a single email inbox and staff manually categorise and assign each one. We want to automate the triage: classify the complaint, assign it to the right department, generate an acknowledgement to the complainant, and flag anything that looks urgent. The tricky part is that our public sends messages in very mixed Arabic and English, sometimes just a few words, and sometimes a very detailed paragraph. We also get spam and off-topic messages that we need to filter out before they reach our staff."

**What to think about:** How do you handle very short or ambiguous inputs ("the road is broken near my house")? What does urgency mean for a public services context — how is it different from the support triage in Project 4? How do you handle Arabic, English, and mixed-language inputs? What is the right way to generate an acknowledgement that sounds like it came from a government body?

---

## Evaluation Criteria

Your submission will be assessed on the following.

### Problem Understanding

Did you correctly identify what the client actually needs? Did you surface the constraints and risks that are not explicitly stated in the brief? Did you make sensible assumptions where the brief was vague, and did you state those assumptions clearly?

### Design Decisions

Are your architectural choices justified? Did you select the right components from the watsonx stack for the task? Where you had options (e.g. agent vs. pipeline, RAG vs. fine-tuning), can you explain why you chose what you chose?

### Safety and Governance

Does your solution include at least one safety mechanism appropriate to the domain? Is there an audit or governance layer? Did you identify the domain-specific risks (the risks in a medical triage system are different from those in a complaint handler) and address them specifically?

### Scope Management

Did you define a realistic scope for two weeks? Did you identify what you left out and why? A well-scoped partial solution is better than an overambitious incomplete one.

### Working Implementation

Does the core capability function? Can a reviewer see the system doing something real?

### Presentation

Can you explain your decisions under questioning? Can you articulate what you would do differently if you had more time or a real client's data?

---

## A Note on Using Prior Work

You are expected to draw on everything from Projects 1–6. Reusing code, patterns, and mock documents from earlier projects is not only allowed — it is encouraged. A real engagement builds on what you already know. What is not acceptable is treating a prior project as a drop-in solution without thinking about whether it fits the new context. The capstone is a new problem with new constraints. Prior work is a starting point, not an answer.

---

## Timeline Suggestion

Two weeks is not much time. Here is a rough allocation to consider — you can deviate from it, but if you do, explain why in your discovery document.

| Days | Focus                                                                                          |
| ---- | ---------------------------------------------------------------------------------------------- |
| 1–2  | Discovery: read the brief, define scope, write the discovery document, sketch the architecture |
| 3–7  | Build: implement the core capability and at least one safety/governance mechanism              |
| 8–9  | Test and document: build your test cases, write up what works and what doesn't                 |
| 10   | Presentation preparation                                                                       |

The biggest mistake trainees make on open-ended projects is spending too long in the build phase and not leaving enough time to reflect, document, and prepare to present. A system you cannot explain is not a finished system.
