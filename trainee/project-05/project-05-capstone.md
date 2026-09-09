# Project 5: Capstone — Client Brief

**Stack:** Your choice  
**Duration:** ~3.5 weeks (18 working days)  
**Difficulty:** Capstone  
**Reference material:** [`mock-docs/`](mock-docs/) — example documents, one subfolder per example scenario. **For reference only — see below.**

---

## What This Project Is

The previous four projects gave you a problem, a plan, and told you what to build. This one does not.

You must identify a real business problem yourself, decide what to build, design the system, build it, and present it — the same way you would in a real engagement. Finding and framing the problem is part of the work. Nobody will hand you a brief. Part of what you are being assessed on is how you handle that ambiguity: the problem you choose, the questions you would ask the client, the assumptions you make explicit, and the decisions you justify.

Your problem must sit in one of the four sectors that matter most to the Kuwait market:

- **Government** — ministries, municipalities, and public-sector bodies
- **Banking** — regulated retail and Islamic finance institutions
- **Cross-sector (private business)** — the large private conglomerates and retail groups that touch everyday life in Kuwait (e.g. Al Shaya, Alghanim Industries, Xcite)
- **Oil** — national and operational entities in the oil and energy sector

> **The example scenarios and mock documents in this project are for reference only.** They show the *shape* of a good capstone problem — a specific client, a real pain, sector-specific constraints, and a reason AI is the right tool — and the *kind* of source material you would need. They are not a menu. You must come up with your own problem, write your own client brief, and create your own mock data. Do not build one of the example scenarios as-is.

Concretely, this means you will:

- **Pick a sector and a specific client type** (a ministry, a bank, a retail group, an oil operator) and identify a real, concrete problem they face today. Ground it in something you can point to: a process you have seen, a public complaint, a regulation, a news story, a conversation with someone who works there.
- **Write the client brief yourself**, in the client's voice, at roughly the level of detail of the examples below. It should be honest about the constraints — regulation, liability, language, data sensitivity — that make the problem hard.
- **Create your own mock documents and data** for the system to work over. The `mock-docs/` folders show what this looks like; yours should be built for *your* problem.
- **Agree your problem with your mentor by the end of Day 3**, alongside your discovery document. No two trainees in the same cohort may work on the same problem.

Use the examples to calibrate ambition and specificity. If your problem is vaguer than the examples, sharpen it. If your client could be swapped for any other company without changing the brief, it is not sector-specific enough.

You are free to use AI tools to help design and build your solution — that reflects how this work actually gets done. What you will be scrutinised on is not whether you typed every line yourself, but whether **you** understood the sector, made deliberate design choices, can justify every decision you made, and can present and defend the result convincingly. A working demo that you cannot explain, or that does not reflect a real understanding of the sector's constraints, will score worse than a smaller solution you can defend under hard questioning. Treat the presentation as a pitch: your job is to convince the evaluators that this is a use case their sector would actually want, not just that the AI works.

---

## What You Must Produce

Unlike earlier projects, there is no prescribed deliverable structure. You decide what to build and how to present it. At minimum, your submission must include:

### 1. Discovery Document

Before writing any code, produce a one-to-two page document covering:

- The client brief you wrote — who the client is, what they are asking for, in their voice
- Your interpretation of the client's problem — what are they actually trying to solve?
- Why this is a genuine, current problem for this sector in Kuwait, and why AI is the right tool for it
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

Present your solution to your mentor as if you are presenting to the client. Structure the presentation as a pitch, not a walkthrough:

1. **Frame the business problem first.** Before showing any system, state the problem you identified, why it matters to this sector, and what it costs the client today (time, money, risk, reputation) if it goes unsolved. Do not open with the tool — open with the pain.
2. **Then demo the solution against that problem.** Walk through your working system so the evaluators can see, concretely, how each part of the demo answers the problem you just framed — not a generic feature tour.
3. **Close with what works, what doesn't, and what you would do next.**

You will be asked questions. The ability to defend your decisions under questioning is part of the assessment.

---

## Example Client Scenarios (Reference Only)

> **Reminder:** these are worked examples of what a capstone problem looks like, not a list to choose from. Read them to understand the level of specificity, the kind of constraints to surface, and the "what to think about" questions you should be asking about your own problem. Then define your own. The matching `mock-docs/` folders exist so you can see what reference material for a problem like this looks like — build your own equivalent for yours.

---

### Scenario A — Ministry of Commerce: Business Licensing Assistant *(Sector: Government)*

**The brief:**

> "We handle hundreds of enquiries every day from business owners asking about licensing requirements, required documents, fees, and renewal procedures. Our staff spend most of their time answering the same questions repeatedly instead of handling complex cases. We want an AI assistant that can handle routine enquiries so our staff can focus on the work that actually needs a human. We have a large internal manual that covers most of what people ask about, but it hasn't been updated consistently and some sections are outdated. We also want to make sure we know what the AI is telling people — if it gives wrong advice about a legal requirement, that is a serious problem for us."

**What to think about:** What happens when the AI's source documents are outdated? Who is liable when AI gives incorrect regulatory guidance? What queries absolutely must not be handled without a human? How do you build trust with a government client who has never deployed AI before?

---

### Scenario B — Burgan-style Retail Bank: Islamic Finance Product Advisor *(Sector: Banking)*

**The brief:**

> "Our customers often don't understand the difference between our Murabaha, Ijara, and Tawarruq products. They call our contact centre, wait on hold, and still leave confused. We want a digital assistant that can explain our products in plain language, help customers understand which product might suit their situation, and guide them to apply. We are a regulated entity — we cannot give financial advice, and we cannot make promises about approval. The assistant must stay within those boundaries. We also have customers who speak Arabic and customers who speak English, sometimes in the same message."

**What to think about:** Where is the line between product information and financial advice? How do you handle code-switching (Arabic/English in the same query)? What does "cannot make promises about approval" mean for the system's outputs? What governance is required for a financial services AI in Kuwait?

---

### Scenario C — Kuwait Oil Company Field Operations *(Sector: Oil)*

**The brief:**

> "Our field engineers carry hundreds of technical manuals, maintenance procedures, and safety protocols. When something goes wrong at 2am, they need answers fast and they cannot search through PDFs on a tablet in the dark. We want a mobile-friendly assistant that can answer questions from our technical documentation. The safety-critical part is important: some of our procedures have very specific steps that must be followed in order, and an AI that paraphrases or skips a step could cause an accident. We also have documentation at different sensitivity levels — general maintenance procedures are fine to share widely, but some operational data is restricted to senior engineers."

**What to think about:** How do you handle procedural content where order and completeness matter? What does "paraphrasing" a safety procedure mean for the system design? How do you implement document-level access control? What does a failure in this system look like, and what is the cost?

---

### Scenario D — Alghanim Industries-style Conglomerate: Multi-Brand Customer Care Assistant *(Sector: Cross-sector / Private Business)*

**The brief:**

> "We operate dozens of brands across automotive, electronics, and consumer goods — think Toyota, Yiaco, and our retail chains, all under one group. Customers call or message about warranty claims, service bookings, and product questions, but which brand and which policy applies is different every time. Our contact centre agents currently have to look up the right brand's policy manually before they can even start helping. We want an AI assistant that can identify which brand and product a customer is asking about, apply the right policy, and either resolve simple requests directly or hand off to the right brand's team with full context. We cannot have the assistant quote a warranty term from the wrong brand, and we cannot have it make commitments — like promising a refund or a replacement — that only a human with approval authority can make."

**What to think about:** How do you keep dozens of brand policies from bleeding into each other? What does "cannot make commitments" mean for how the system is allowed to phrase its responses? How do you decide what a bot can resolve directly versus what must go to a human, and how do you hand off with enough context that the customer doesn't repeat themselves? How would you convince a group like this — used to running many separate brand operations — that a shared AI layer is worth centralising?

---

### Scenario E — Xcite-style Electronics Retailer: Pre-Sale and Post-Sale Product Assistant *(Sector: Cross-sector / Private Business)*

**The brief:**

> "Customers message us on WhatsApp and our website asking whether a product is in stock, how it compares to a competitor's model, whether it's compatible with something they already own, and — after they've bought it — how to get it repaired or exchanged. Our staff are good at this in person but online we lose a lot of customers to slow responses. We want an assistant that can answer pre-sale product questions accurately from our catalogue and specs, and handle post-sale queries like return eligibility and repair status. Our catalogue changes constantly with new stock and promotions, so whatever you build has to reflect what's actually available today, not what we told it last month. We're also worried about the assistant confidently inventing a spec or a promotion that doesn't exist — that's the kind of mistake that ends up as a public complaint."

**What to think about:** How do you keep a fast-changing catalogue and promotions from going stale in the AI's knowledge? What guardrails stop the system from inventing a spec, price, or promotion it isn't sure about? Where is the line between "pre-sale product advice" and something that starts to look like a purchase commitment the company has to honour? How would you pitch the ROI of this to a retail group that measures everything by conversion and complaint volume?

---

### Scenario F — Kuwait Municipality: Public Services Complaint Handler *(Sector: Government)*

**The brief:**

> "We receive thousands of complaints and service requests from the public every week — potholes, broken streetlights, waste collection issues, noise complaints. Right now everything comes in through a single email inbox and staff manually categorise and assign each one. We want to automate the triage: classify the complaint, assign it to the right department, generate an acknowledgement to the complainant, and flag anything that looks urgent. The tricky part is that our public sends messages in very mixed Arabic and English, sometimes just a few words, and sometimes a very detailed paragraph. We also get spam and off-topic messages that we need to filter out before they reach our staff."

**What to think about:** How do you handle very short or ambiguous inputs ("the road is broken near my house")? What does urgency mean for a public services context — how is it different from the support triage pipeline in Project 2? How do you handle Arabic, English, and mixed-language inputs? What is the right way to generate an acknowledgement that sounds like it came from a government body?

---

## Evaluation Criteria

Your submission will be assessed on the following.

### Problem Understanding

Did you choose a real, specific problem that a client in this sector actually has? Did you correctly identify what the client actually needs — not just what they asked for? Did you surface the constraints and risks that are not explicitly stated in your brief? Did you make sensible assumptions where things were vague, and did you state those assumptions clearly? A problem that was invented to fit a system you already wanted to build will be obvious, and will score poorly.

### Sector Relevance and Persuasiveness

Would a real stakeholder in this sector — a government official, a bank compliance officer, a conglomerate operations lead, an oil company safety engineer — recognise this as a genuine, relevant use case for their world, not a generic chatbot with the sector's name attached? Did you understand what makes this sector distinct (regulation, risk tolerance, brand structure, public accountability)? Could you convince a sceptical evaluator playing that stakeholder that this is worth building?

### Design Decisions

Are your architectural choices justified? Did you select the right components from the watsonx stack for the task? Where you had options (e.g. agent vs. pipeline, RAG vs. fine-tuning), can you explain why you chose what you chose?

### Safety and Governance

Does your solution include at least one safety mechanism appropriate to the domain? Is there an audit or governance layer? Did you identify the domain-specific risks (the risks in a safety-critical oil operations assistant are different from those in a retail product assistant) and address them specifically?

### Scope Management

Did you define a realistic scope for ~3.5 weeks? Did you identify what you left out and why? A well-scoped partial solution is better than an overambitious incomplete one.

### Working Implementation

Does the core capability function? Can a reviewer see the system doing something real?

### Presentation

Can you explain your decisions under questioning? Can you articulate what you would do differently if you had more time or a real client's data?

---

## A Note on Using Prior Work

You are expected to draw on everything from Projects 1–4. Reusing code, patterns, and techniques from earlier projects is not only allowed — it is encouraged. The example mock documents in this project may be used as templates for the format and depth of your own, but the content your system runs on must be yours, built for your problem. A real engagement builds on what you already know. What is not acceptable is treating a prior project as a drop-in solution without thinking about whether it fits the new context. The capstone is a new problem with new constraints. Prior work is a starting point, not an answer.

---

## Timeline Suggestion

Eighteen working days is not much time for an open-ended engagement. Here is a rough allocation to consider — you can deviate from it, but if you do, explain why in your discovery document.

| Days  | Focus                                                                                          |
| ----- | ---------------------------------------------------------------------------------------------- |
| 1–3   | Discovery: identify your problem, write the client brief, define scope, write the discovery document, agree it with your mentor, sketch the architecture |
| 4–13  | Build: implement the core capability and at least one safety/governance mechanism              |
| 14–16 | Test and document: build your test cases, write up what works and what doesn't                 |
| 17–18 | Presentation preparation                                                                       |

The biggest mistake trainees make on open-ended projects is spending too long in the build phase and not leaving enough time to reflect, document, and prepare to present. A system you cannot explain is not a finished system.

---

## Practitioner Resources

Grouped by the stage of the capstone they help with. You are not expected to read all of them — pick what your problem needs.

### Finding and framing your problem

- [People + AI Guidebook: User Needs + Defining Success](https://pair.withgoogle.com/chapter/user-needs/) — Google's guide to finding problems AI is genuinely suited to, deciding between automating and augmenting a task, and defining what success looks like before you build. Use it to test whether your problem actually needs AI.
- [AI Product Discovery Frameworks: How AI Is Changing the Way Teams Build](https://www.productboard.com/blog/ai-product-discovery-frameworks/) — overview of discovery frameworks (JTBD, RICE, opportunity trees) useful for choosing which problem to solve and why.
- [Working Backwards PR/FAQ: Instructions and Template](https://workingbackwards.com/resources/working-backwards-pr-faq/) — Amazon's method of writing the announcement and the hard questions *before* building anything. A good template for writing your client brief and discovery document in the client's voice.
- [Putting Amazon's PR/FAQ to Practice](https://commoncog.com/putting-amazons-pr-faq-to-practice/) — an honest worked example of using PR/FAQ on a small team, including the five questions it forces you to answer (who is the customer, what is the problem, what is the solution, why would they adopt it, how big is it).

### Scoping the build

- [Evolution, Cupcakes, and Skeletons](https://www.industriallogic.com/blog/evolution-cupcakes-and-skeletons/) — the "walking skeleton" idea: get a thin end-to-end slice working first, then thicken it. The single most useful scoping technique for an 18-day build.

### Designing the architecture

- [C4 Model: Introduction](https://c4model.com/introduction) — a simple, notation-independent way to draw architecture at different zoom levels (context, containers, components). Use the context and container levels for your architecture diagram.
- [Patterns for Building LLM-based Systems and Products](https://eugeneyan.com/writing/llm-patterns/) — seven practical patterns (evals, RAG, fine-tuning, caching, guardrails, defensive UX, user feedback) with the trade-offs of each. Read this when justifying your design choices.
- For the agent-versus-pipeline decision, revisit the resources in Project 2.

### Testing and evidence

- [Your AI Product Needs Evals](https://hamel.dev/blog/posts/evals/) — why AI products fail without a problem-specific evaluation system, and how to build one at three levels (unit tests, human/model review, A/B). Directly applicable to your test evidence deliverable.
- [Ragas: Generate a Synthetic Test Set for RAG](https://docs.ragas.io/en/stable/getstarted/rag_testset_generation/) — how to generate question/answer test cases from your own mock documents, so you can test at scale rather than by hand.

### Safety and governance

- [OWASP Top 10 for LLM Applications 2025](https://genai.owasp.org/resource/owasp-top-10-for-llm-applications-2025/) — the standard list of LLM application risks (prompt injection, sensitive data disclosure, excessive agency, misinformation). Use it as a checklist when deciding which safety mechanism your domain needs most.
- [LLM Guardrails: Best Practices for Deploying LLM Apps Securely](https://www.datadoghq.com/blog/llm-guardrails-best-practices/) — concrete input/output guardrail patterns, applicable to any safety-critical assistant.
- [LLM Guardrails: Securing Large Language Models for Real-World Use](https://witness.ai/blog/llm-guardrails/) — broad, vendor-neutral rundown of guardrail types and why they matter for regulated/safety-critical deployments.

### Kuwait sector context

- [AI Regulation in Kuwait: A Practical Guide](https://www.levellers.ai/what-is/ai-regulation-kuwait) — how AI is currently governed in Kuwait through existing law (CITRA, the Central Bank, cybercrime statutes) rather than a dedicated AI act. Essential background for the "constraints and risks" section of your discovery document.
- [Kuwait National AI Strategy 2025–2028: Overview](https://digital.nemko.com/regulations/kuwait-ai-regulation) — the government's stated priorities for AI across sectors. Use it to show that your problem is one the country is actually trying to solve.
- [Kuwait Data Privacy Protection Regulation (CITRA Resolution 42 of 2021)](https://securiti.ai/kuwait-data-privacy-protection-regulation/) — what the data protection rules require of anyone collecting or processing personal data in Kuwait: consent, breach notification, data subject rights. Relevant to any capstone that touches customer or citizen data.
- [Central Bank of Kuwait: Digital Banks Guidelines](https://www.cbk.gov.kw/en/cbk-news/announcements-and-press-releases/press-releases/2022/02/202202021000-cbk-governor-announces-digital-banks-guidelines) — the regulator's own announcement of its digital banking framework. A starting point for understanding how the CBK thinks about risk in banking technology.
- [Kuwait Advances Digital Transformation with Secure Cyber Infrastructure](https://timeskuwait.com/kuwait-advances-digital-transformation-with-secure-cyber-infrastructure/) — where government digital services (Sahel, Hawiyati) stand today and where AI is expected to go next. Useful for grounding a government-sector problem in something real.
- [Arabic NLP — How To Overcome Challenges, Tutorials In Python & 9 Tools/Resources](https://spotintelligence.com/2023/10/29/arabic-nlp/) — explains dialect variation, morphology, and tooling gaps, key background for any problem with mixed Arabic/English input.

### Presenting and defending your work

- [Peter Cohan on "Do the Last Thing First" in a Software Demo](https://www.reprise.com/resources/blog/peter-cohan-on-how-to-get-the-end-result-in-a-software-demo) — show the end result before the process. The most effective single change you can make to a 15-minute pitch demo.
- [A Framework For Presenting Complex Machine Learning Concepts for Non-Technical Stakeholders](https://www.ninetwothree.co/resources/a-framework-for-presenting-complex-machine-learning-concepts-for-non-technical-stakeholders) — practical guidance on audience-tailored updates, demo cadence, and avoiding overpromising accuracy when pitching an AI solution.
- [How to Communicate with Non-Technical Stakeholders](https://qat.com/how-to-communicate-with-non-technical-stakeholders/) — six concrete tips (jargon-free language, business framing, visuals) directly applicable to a client-facing capstone presentation.
