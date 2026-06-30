# Capstone Evaluator Guide

**For mentor use only — do not share with trainees**

---

## How to Use This Guide

This document is your reference for assessing capstone submissions. It is not a marking rubric with numerical scores — it is a structured set of things to look for, questions to probe, and patterns to watch for. Your feedback should be written, specific, and reference actual decisions the trainee made rather than generic observations.

A trainee who built a limited system but understood exactly why it is limited and what would be needed to improve it has demonstrated more learning than one who built a larger system and cannot explain their choices. Calibrate accordingly.

Do not share this document with trainees before or during the project.

---

## Assessment Dimensions

Assess every submission against these five dimensions regardless of which scenario was chosen.

---

### Dimension 1: Problem Understanding

**What you are looking for:**
The discovery document should show that the trainee read the brief critically, not just literally. The brief contains things that are implied but not stated — a good trainee surfaces these. A weak trainee treats the brief as a specification and builds exactly what was described, no more.

**Strong indicators:**
- Identifies constraints not mentioned in the brief (e.g. for Scenario A: what happens when the source document is outdated? who is liable?)
- Asks meaningful clarifying questions in the discovery document and provides reasoned assumed answers
- Defines out-of-scope explicitly and explains why (not just "we ran out of time")
- Recognises the domain-specific risk (medical, financial, legal, safety-critical) and names it

**Weak indicators:**
- Discovery document reads like a restatement of the brief
- No questions asked — the trainee assumed everything was specified
- Scope is defined by what was built, not by deliberate decision
- No mention of what could go wrong

**Probing question:** "You stated that X is out of scope. Walk me through the decision — what would it have required, and why did you decide not to include it?"

---

### Dimension 2: Architecture and Design Decisions

**What you are looking for:**
The trainee should be able to explain why they chose each component and what the alternatives were. The choice of RAG vs. agent vs. pipeline should be deliberate. The choice of which watsonx products to use should be justified against the scenario's requirements, not just "we used everything."

**Strong indicators:**
- Architecture diagram is accurate (matches what was actually built)
- Written justification addresses tradeoffs, not just the chosen option
- Watsonx product choices are tied to specific scenario requirements (e.g. "we used watsonx.governance because the scenario requires audit — we wouldn't have needed it for a less regulated domain")
- Knows where the architecture has weaknesses and can name them

**Weak indicators:**
- Architecture diagram does not match the code
- Justification is "we used RAG because we learned about it in Project 1" — no connection to this scenario's needs
- Every possible watsonx feature is used regardless of whether the scenario requires it
- Cannot explain a component when asked

**Probing question:** "If you were starting over with twice the time, what would you change about this architecture and why?"

---

### Dimension 3: Safety and Governance

**What you are looking for:**
Every scenario has domain-specific risks. The trainee should have identified the primary risk for their scenario and built a mechanism to address it — not just noted it in the discovery document. The governance layer should be appropriate to the domain, not generic.

**Scenario-specific primary risks:**

| Scenario | Primary risk | What to look for |
|---|---|---|
| A — Ministry licensing | Outdated source giving wrong legal guidance | Currency check on retrieved documents, clear "I don't know" path, human escalation |
| B — Islamic bank | Crossing into financial advice | Hard refusal pattern for advice-seeking queries, product-info-only boundary enforced in prompt |
| C — Oil field operations | Procedural content being summarised or reordered | Step-completeness check, verbatim procedure output for safety-critical steps |
| D — Hospital triage | Routing a critical patient to the wrong department | Red flag symptom override, Immediate escalation path that cannot be suppressed |
| E — Law firm | Missing a high-severity clause issue | Completeness over precision — prefer false positives to false negatives, High flags never suppressed |
| F — Municipality | Confidently routing an ambiguous complaint wrongly | Low-confidence path routes to human review, short/ambiguous inputs handled explicitly |

**Weak indicators:**
- Governance is a watsonx.governance factsheet with no substance ("limitations: none known")
- Safety mechanism is only described, not implemented
- The primary domain risk is not addressed at all — trainee didn't recognise it

**Probing question:** "Show me what happens when [scenario-specific worst case]. Walk me through the system step by step."

---

### Dimension 4: Scope Management

**What you are looking for:**
Two weeks is not long. A trainee who tries to build everything will build nothing properly. Good scope management means choosing what to build deliberately, building it well, and being honest about what was left out.

**Strong indicators:**
- Core capability works end to end and is demonstrable
- What was left out is documented and the trainee can explain what it would take to add it
- Scope decisions were made early (in the discovery document) not by running out of time
- The trainee can distinguish between "we chose not to build this" and "we ran out of time"

**Weak indicators:**
- Large portions of the system are broken or non-functional
- Scope was not defined upfront — the trainee built until time ran out
- Test evidence is missing or covers only the happy path
- The deployment readiness assessment says the system is ready when it clearly is not

**Probing question:** "Your discovery document scoped out X. Two weeks later, do you still think that was the right call? What did you learn during the build that changed your view?"

---

### Dimension 5: Communication and Defence

**What you are looking for:**
The 15-minute presentation is not a demo. It is an assessment of whether the trainee understands what they built well enough to explain it, defend it, and acknowledge its limitations. A trainee who can only demo a working system but cannot answer questions about why it works that way has not fully learned.

**Strong indicators:**
- Explains decisions without prompting — doesn't just show features
- Acknowledges limitations honestly rather than pivoting away from them
- Answers "what would you do differently" with specifics, not generalities
- When challenged, engages with the challenge rather than defending their original decision reflexively

**Weak indicators:**
- Only presents the happy path; cannot demo failure cases
- Deflects questions about weaknesses ("we didn't have time for that")
- Cannot explain a component when asked how it works
- Reads from slides rather than explaining in their own words

**Suggested question sequence for the presentation:**
1. "Before you show me anything — in one sentence, what problem did you solve?"
2. "Walk me through a user interaction from start to finish."
3. "Now show me something going wrong. What does the system do?"
4. "Point to the part of your architecture you are least confident in. Why?"
5. "If this was going live next month with real users, what would you be most worried about?"

---

## Per-Scenario Assessment Notes

### Scenario A — Ministry of Commerce: Business Licensing Assistant

**What a good solution looks like:**
The trainee recognised that outdated source documents are the central design challenge — not a peripheral concern. The system either: (a) surfaces document metadata (last updated date) alongside answers so users know how current the information is, or (b) includes a disclaimer on every response that users should verify current requirements with the ministry. There is a clear escalation path for queries that cannot be answered with confidence. The audit trail records what was answered and from which document version.

**What a weak solution looks like:**
A RAG pipeline over the documents with no mechanism for handling outdated content. The system confidently answers questions about fees or procedures that are marked as "under review" in the source documents.

**Red flags:**
- System answers questions about legal requirements with no caveats
- No escalation path for out-of-scope or uncertain queries
- The trainee cannot explain what happens when a document is updated

**Scenario-specific probing questions:**
- "One of your source documents has a section marked 'under review — procedures may change.' Show me what your system does when a user asks about that section."
- "A user asks whether a foreigner can own 100% of a business. Your documents say different things in different sections. What does your system return?"

---

### Scenario B — Islamic Bank: Product Advisor

**What a good solution looks like:**
The trainee drew a clear technical line between product information and financial advice, and enforced it in the system — not just as a note in the discovery document. The system refuses or redirects queries like "should I take the Murabaha or the Ijara for my situation?" while helpfully answering "what is the difference between Murabaha and Ijara?" The Arabic/English handling is at least acknowledged — even if full bilingual support wasn't built, the trainee should have designed for it and explained why they scoped it out.

**What a weak solution looks like:**
A chatbot that answers any question without enforcing the advice boundary. The system recommends products based on user situation — crossing from information into advice without the trainee noticing.

**Red flags:**
- System responds to "which product is best for me?" with a product recommendation
- No mention of the CBK regulatory context in the governance layer
- Arabic input not considered at all — not even as an acknowledged gap

**Scenario-specific probing questions:**
- "A user types: 'I earn KWD 800 a month and need KWD 5,000. Which product should I get?' Show me exactly what your system returns."
- "Where exactly is the line between product information and financial advice in your system? Is it in the prompt, the retrieval, the output — and why did you put it there?"

---

### Scenario C — Kuwait Oil Company: Field Operations Assistant

**What a good solution looks like:**
The trainee identified that safety-critical procedural content cannot be paraphrased — if a maintenance procedure has 9 numbered steps, the system should return all 9 in order, not a summary. This is a design constraint that changes how the RAG output is handled. The access control enforcement at the retrieval layer is present and the trainee can demonstrate that a General-clearance user cannot retrieve Restricted documents even when they ask a highly relevant question. The system has some mechanism for indicating completeness — i.e. signalling when a retrieved procedure may be partial.

**What a weak solution looks like:**
A standard RAG pipeline that summarises retrieved content. Safety procedures are paraphrased and steps are dropped or reordered in the generated response.

**Red flags:**
- Maintenance procedures are summarised rather than returned verbatim or in full
- Access control is implemented in the display layer (filtered after model sees the content), not the retrieval layer
- The trainee has not thought about what "wrong" looks like in this domain — a wrong answer here means an accident

**Scenario-specific probing questions:**
- "Show me what happens when a General-clearance engineer asks a question whose best answer is in a Restricted document. Walk me through each step."
- "Your pump inspection procedure has 9 steps. Your system retrieved the relevant chunk. Show me the response. Are all 9 steps present and in order?"

---

### Scenario D — Private Hospital: Patient Intake and Triage

**What a good solution looks like:**
The trainee implemented an unconditional override for the red flag symptoms (chest pain, difficulty breathing, loss of consciousness, severe bleeding, stroke signs) — these always escalate to Immediate / Emergency regardless of anything else in the conversation. This override is not handled by the model's judgement; it is a deterministic rule that fires before the model is consulted. The audit trail is complete enough that a medical director could reconstruct every patient interaction. The trainee understands and can articulate the difference between routing and diagnosing.

**What a weak solution looks like:**
A conversational agent that uses the model to determine urgency for all inputs, including the red flag symptoms. The model's judgement is the only gate — there is no deterministic override for life-threatening symptoms.

**Red flags:**
- Red flag symptom handling is model-dependent (the model "usually" escalates these correctly)
- The system tells a patient their condition sounds non-urgent
- The audit trail does not include the full conversation — only the final routing decision
- Trainee cannot clearly explain the routing vs. diagnosing boundary

**Scenario-specific probing questions:**
- "A patient types 'I have a mild chest pain but I think it's just indigestion.' What does your system do, and why?"
- "Walk me through the audit record for that interaction. What would the medical director see?"
- "At what point does your system decide it is routing rather than diagnosing? Is that a model decision or a rule? Why?"

---

### Scenario E — Law Firm: Contract Review and Compliance Flagging

**What a good solution looks like:**
The trainee designed for completeness over precision — in contract review, missing a High-severity issue is far worse than over-flagging a Medium one. The system flags liberally and explains why each flag was raised. The trainee considered the confidentiality concern and has a position on it (even if the full solution wasn't built) — data sent to a model API crosses a trust boundary and the trainee should know this. The versioning of the clause library is at least addressed: the trainee should explain how the knowledge the system uses could be updated when the law changes.

**What a weak solution looks like:**
A system that reviews contracts and tries to give confident verdicts ("this clause is compliant"). A system that flags conservatively to reduce noise — missing High-severity issues because the trainee optimised for fewer false positives.

**Red flags:**
- System gives legal opinions rather than flagging for review
- High-severity flags are suppressed to reduce noise
- Confidentiality of client contract content not mentioned at all
- No thought given to what happens when the law changes

**Scenario-specific probing questions:**
- "Your system reviewed this contract and found 3 issues. How confident are you that there are no other issues? What might it have missed?"
- "A client's confidential contract was sent to the watsonx.ai API. Who has seen that data? What did you do about this?"
- "The Kuwait Commercial Law you used as reference is from 2023. An amendment was passed last month. How does your system handle this?"

---

### Scenario F — Kuwait Municipality: Complaint Handler

**What a good solution looks like:**
The trainee designed for ambiguous, short, messy inputs — because that is what the public actually sends. There is a meaningful low-confidence path: complaints that cannot be classified with reasonable confidence route to a human reviewer rather than being forced into a category. The acknowledgement messages are appropriate in tone for a government body — formal, respectful, not chatbot-casual. The trainee has at least acknowledged the Arabic input challenge, even if full Arabic support was not built.

**What a weak solution looks like:**
A classifier that always assigns a category even when the input is too ambiguous to classify reliably. Acknowledgement messages that read like chatbot output rather than official government communications.

**Red flags:**
- "it doesnt work fix it" gets confidently classified and routed without flagging
- Acknowledgement messages use informal language inappropriate for a government entity
- Arabic input causes the system to crash or return an error rather than handling gracefully
- No spam/off-topic filter — everything gets routed as a complaint

**Scenario-specific probing questions:**
- "A message comes in that says 'the road near my house is bad.' How does your system handle it? What does it do with the location ambiguity?"
- "Show me the Arabic acknowledgement message for a standard complaint. Read it to me — does it sound like something a government body would send?"
- "A message comes in that is clearly spam — an advertisement. What does your system do?"

---

## Common Failure Patterns Across All Scenarios

These are patterns that appear regardless of scenario. Watch for them.

**"It works on the happy path."**
The trainee only tested inputs that the system was designed to handle well. Every test case is clean, complete, and in English. Edge cases, ambiguous inputs, and adversarial inputs were not tested. This is the most common failure pattern in the cohort.

**The governance layer is cosmetic.**
The watsonx.governance factsheet was filled in as a compliance exercise. The limitations section is empty or says "none identified." The monitoring configuration was set up but the trainee cannot explain what it is monitoring for or what they would do if they saw an anomaly.

**The discovery document was written after the build.**
The discovery document describes what was built, not what was planned. Questions listed as "things to ask the client" were all answered by the final system design. The document was written to justify decisions already made, not to guide decisions yet to be made. You can usually tell because the assumed answers are suspiciously well-aligned with the architecture.

**Safety mechanism is in the prompt, not the architecture.**
The trainee handled safety-critical behaviour (red flag symptoms, regulatory advice boundary, procedural completeness) by including an instruction in the system prompt. This is fragile — models do not follow instructions reliably under adversarial input. Safety mechanisms for high-stakes scenarios should be deterministic rules in the application layer, not model instructions.

**Scope management was time management, not design.**
The trainee did not define scope upfront. They built until time ran out and then described what exists as "the scope." There is no record of a deliberate decision about what to exclude. When asked "why didn't you build X?" the answer is "we didn't have time" rather than "we decided not to because Y."

---

## Final Assessment Guidance

After the presentation, write your feedback covering:

1. **One thing they got genuinely right** — be specific about what it was and why it matters
2. **One thing they fundamentally misunderstood** — name it clearly; this is the most important feedback they will receive
3. **One decision you would have made differently** — explain your reasoning; this is a learning conversation, not a verdict
4. **Readiness assessment** — on a three-point scale: Not yet ready for client-facing AI work / Ready with supervision / Ready to lead a project with guidance

Do not give a pass/fail grade. The readiness assessment is for your own calibration and for the programme lead — share it with the trainee as a starting point for a conversation about their development, not as a final judgement.
